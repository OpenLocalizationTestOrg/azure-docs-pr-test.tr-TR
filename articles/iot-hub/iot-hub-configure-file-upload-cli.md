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
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a>IOT Hub'ın Azure CLI kullanarak dosya yüklemeleri yapılandırın

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

toouse hello [dosya karşıya yükleme işlevselliği IOT hub'da][lnk-upload], bir Azure Storage hesabı IOT hub'ınıza ilk ilişkilendirmeniz gerekir. Mevcut bir depolama hesabını kullanma veya yeni bir tane oluşturun.

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Etkin bir Azure hesabı. Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.
* [Azure CLI 2.0][lnk-CLI-install].
* Azure IOT hub'ı. IOT hub'ı yoksa, hello kullanabilirsiniz `az iot hub create` [komutu] [ lnk-cli-create-iothub] toocreate bir ya da kullanım hello portal çok [IOT hub'ı Oluştur] [lnk-portal-hub].
* Bir Azure depolama hesabı. Bir Azure depolama hesabınız yoksa, hello kullanabilirsiniz [Azure CLI 2.0 - depolama hesaplarını yönetme] [ lnk-manage-storage] toocreate bir ya da kullanım hello portal çok[depolama hesabı oluşturma] [lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>Oturum açma ve Azure hesabınızı ayarlama

Tooyour Azure hesabı oturum ve aboneliğinizi seçin.

1. Merhaba Hello komut isteminde çalıştırmak [oturum açma komut][lnk-login-command]:

    ```azurecli
    az login
    ```

    Merhaba yönergeleri tooauthenticate Hello kod kullanarak izleyin ve oturum açma tooyour bir web tarayıcısı aracılığıyla Azure hesabı.

1. Birden çok Azure aboneliğiniz varsa tooAzure imzalama tooall erişim verir kimlik bilgilerinizle ilişkili Azure hesapları hello. Merhaba aşağıdaki kullanın [komutu toolist hello Azure hesapları] [ lnk-az-account-command] , toouse için kullanılabilir:

    ```azurecli
    az account list
    ```

    IOT hub'ınızı toocreate toouse toorun hello komutları istediğiniz komut tooselect abonelik aşağıdaki hello kullanın. Merhaba hello önceki komutunun çıktısından hello abonelik adı veya kimliği kullanabilirsiniz:

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a>Depolama hesabı ayrıntıları alma

Merhaba aşağıdaki adımlarda hello kullanarak depolama hesabınıza oluşturulan varsayılmaktadır **Resource Manager** dağıtım modeli ve değil hello **Klasik** dağıtım modeli.

cihazlarınızın tooconfigure dosya yüklemeleri, hello bağlantı dizesi için bir Azure depolama hesabı gerekiyor. Merhaba depolama hesabı hello olmalıdır IOT hub'ınızı aynı abonelik. Merhaba depolama hesabındaki bir blob kapsayıcısını hello adı da gerekir. Komut tooretrieve aşağıdaki hello depolama hesabı anahtarları kullanın:

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

Merhaba Not **connectionString** değeri. Aşağıdaki adımları hello gerekir.

Var olan bir blob kapsayıcı, dosya yüklemeleri için kullanabilir veya yeni bir tane oluşturun:

* toolist hello mevcut blob kapsayıcıları depolama hesabınızdaki hello aşağıdaki komutu kullanın:

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* Depolama hesabınız, komutu aşağıdaki kullanım hello blob kapsayıcısında toocreate:

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a>Karşıya dosya yükleme

Artık IOT hub tooenable yapılandırabilirsiniz [dosya karşıya yükleme işlevselliği] [ lnk-upload] depolama hesabı bilgilerinizi kullanarak.

Merhaba yapılandırma değerlerini aşağıdaki hello gerektirir:

**Depolama kapsayıcısı**: geçerli, Azure aboneliği tooassociate IOT hub'ınızı ile Azure depolama hesabında blob kapsayıcısı. Önceki bölümde hello hello gerekli depolama hesabı bilgileri alınamadı. Dosyaları karşıya yüklediğinizde IOT Hub cihazları toouse için yazma izinleri toothis blob kapsayıcısı ile SAS URI'ler otomatik olarak oluşturur.

**Karşıya yüklenen dosyalar için bildirimlerin**: etkinleştirmek veya dosya karşıya yükleme bildirimlerini devre dışı.

**SAS TTL**: hello zaman yaşam SAS URI'ler toohello cihaz IOT Hub tarafından döndürülen Merhaba, bu bir ayardır. Tooone saat, varsayılan olarak ayarlayın.

**Dosya bildirim ayarları varsayılan TTL**: hello zaman süresi doldu önce dosya karşıya yükleme bildirimi yaşam. Tooone günü varsayılan olarak ayarlayın.

**Dosya bildirim maksimum teslimat sayısı**: hello sayısı zaman hello IOT hub'ı denemeleri toodeliver dosya karşıya yükleme bildirimi. Too10 varsayılan olarak ayarlayın.

Azure CLI komutları tooconfigure hello dosya karşıya yükleme ayarları, IOT hub'ına aşağıdaki hello kullan:

Bir bash Kabuğu'nu kullanın:

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

Windows komut istemi kullanın:

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

Komutu aşağıdaki hello kullanarak, IOT hub'ına hello dosya karşıya yükleme yapılandırmasını gözden geçirebilirsiniz:

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a>Sonraki adımlar

IOT hub'ı hello dosya karşıya yükleme özellikleri hakkında daha fazla bilgi için bkz: [karşıya bir aygıtı dosyalarından][lnk-upload].

Azure IOT hub'ı yönetme hakkında daha fazla bu bağlantılar toolearn izleyin:

* [Toplu IOT cihazları yönetme][lnk-bulk]
* [IOT hub'ı ölçümleri][lnk-metrics]
* [İzleme işlemleri][lnk-monitor]

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [IOT Hub Geliştirici Kılavuzu][lnk-devguide]
* [Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]
* [IOT çözümünüzden plan hello güvenli][lnk-securing]

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