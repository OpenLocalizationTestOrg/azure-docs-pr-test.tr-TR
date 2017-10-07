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
# <a name="configure-iot-hub-file-uploads-using-powershell"></a>IOT Hub'ın PowerShell kullanarak dosya yüklemeleri yapılandırın

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

toouse hello [dosya karşıya yükleme işlevselliği IOT hub'da][lnk-upload], IOT hub'ınıza ilk Azure storage hesabı ilişkilendirmelisiniz. Mevcut bir depolama hesabını kullanma veya yeni bir tane oluşturun.

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Etkin bir Azure hesabı. Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.
* [Azure PowerShell cmdlet'leri][lnk-powershell-install].
* Azure IOT hub'ı. IOT hub'ı yoksa, hello kullanabilirsiniz [yeni AzureRmIoTHub cmdlet] [ lnk-powershell-iothub] toocreate bir ya da kullanım hello portal çok[IOT hub oluşturma] [ lnk-portal-hub].
* Bir Azure depolama hesabı. Bir Azure depolama hesabınız yoksa, hello kullanabilirsiniz [Azure Storage PowerShell cmdlet'lerini] [ lnk-powershell-storage] toocreate bir ya da kullanım hello portal çok[depolama hesabı oluşturma] [ lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>Oturum açma ve Azure hesabınızı ayarlama

Tooyour Azure hesabı oturum ve aboneliğinizi seçin.

1. Merhaba Hello PowerShell isteminde çalıştırın **Login-AzureRmAccount** cmdlet:

    ```powershell
    Login-AzureRmAccount
    ```

1. Birden çok Azure aboneliğiniz varsa tooAzure imzalama tooall erişim verir kimlik bilgilerinizle ilişkili Azure abonelik hello. Toouse toolist hello Azure abonelikleri kullanılabilir sizin için komutu aşağıdaki hello kullan:

    ```powershell
    Get-AzureRMSubscription
    ```

    IOT hub'ınızı toomanage toouse toorun hello komutları istediğiniz komut tooselect abonelik aşağıdaki hello kullanın. Merhaba hello önceki komutunun çıktısından hello abonelik adı veya kimliği kullanabilirsiniz:

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a>Depolama hesabı ayrıntıları alma

Merhaba aşağıdaki adımlarda hello kullanarak depolama hesabınıza oluşturulan varsayılmaktadır **Resource Manager** dağıtım modeli ve değil hello **Klasik** dağıtım modeli.

cihazlarınızın tooconfigure dosya yüklemeleri, hello bağlantı dizesi için bir Azure depolama hesabı gerekiyor. Merhaba depolama hesabı hello olmalıdır IOT hub'ınızı aynı abonelik. Merhaba depolama hesabındaki bir blob kapsayıcısını hello adı da gerekir. Komut tooretrieve aşağıdaki hello depolama hesabı anahtarları kullanın:

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

Merhaba Not **key1** depolama hesabı anahtar değeri. Aşağıdaki adımları hello gerekir.

Var olan bir blob kapsayıcı, dosya yüklemeleri için kullanabilir veya yeni bir tane oluşturun:

* toolist hello mevcut blob kapsayıcıları depolama hesabınızdaki hello aşağıdaki komutları kullanın:

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* Depolama hesabınız, aşağıdaki komutları kullanın hello blob kapsayıcısında toocreate:

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a>IOT hub'ınızı yapılandırma

Artık IOT hub tooenable yapılandırabilirsiniz [dosya karşıya yükleme işlevselliği] [ lnk-upload] depolama hesabı bilgilerinizi kullanarak.

Merhaba yapılandırma değerlerini aşağıdaki hello gerektirir:

**Depolama kapsayıcısı**: geçerli, Azure aboneliği tooassociate IOT hub'ınızı ile Azure depolama hesabında blob kapsayıcısı. Önceki bölümde hello hello gerekli depolama hesabı bilgileri alınamadı. Dosyaları karşıya yüklediğinizde IOT Hub cihazları toouse için yazma izinleri toothis blob kapsayıcısı ile SAS URI'ler otomatik olarak oluşturur.

**Karşıya yüklenen dosyalar için bildirimlerin**: etkinleştirmek veya dosya karşıya yükleme bildirimlerini devre dışı.

**SAS TTL**: hello zaman yaşam SAS URI'ler toohello cihaz IOT Hub tarafından döndürülen Merhaba, bu bir ayardır. Tooone saat, varsayılan olarak ayarlayın.

**Dosya bildirim ayarları varsayılan TTL**: hello zaman süresi doldu önce dosya karşıya yükleme bildirimi yaşam. Tooone günü varsayılan olarak ayarlayın.

**Dosya bildirim maksimum teslimat sayısı**: hello sayısı zaman hello IOT hub'ı denemeleri toodeliver dosya karşıya yükleme bildirimi. Too10 varsayılan olarak ayarlayın.

PowerShell cmdlet tooconfigure hello dosya karşıya yükleme ayarları, IOT hub'ına aşağıdaki hello kullan:

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