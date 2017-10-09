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
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a>Merhaba yeni AzureRmIotHub cmdlet'ini kullanarak IOT hub oluşturma

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Giriş

Azure PowerShell cmdlet'leri toocreate kullanın ve Azure IOT hub'ları yönetin. Bu öğretici şunların nasıl yapıldığını gösterir toocreate PowerShell ile bir IOT hub.

> [!NOTE]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Azure Resource Manager dağıtım modeli kullanılarak yer almaktadır.

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Etkin bir Azure hesabı. <br/>Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.
* [Azure PowerShell cmdlet'leri][lnk-powershell-install].

## <a name="connect-tooyour-azure-subscription"></a>Tooyour Azure aboneliğine bağlanma
PowerShell komut isteminde tooyour Azure aboneliği içindeki komut toosign aşağıdaki hello girin:

```powershell
Login-AzureRmAccount
```

Birden çok Azure aboneliğiniz varsa tooAzure imzalama tooall erişim verir kimlik bilgilerinizle ilişkili Azure abonelik hello. Toouse toolist hello Azure abonelikleri kullanılabilir sizin için komutu aşağıdaki hello kullan:

```powershell
Get-AzureRMSubscription
```

IOT hub'ınızı toocreate toouse toorun hello komutları istediğiniz komut tooselect abonelik aşağıdaki hello kullanın. Merhaba hello önceki komutunun çıktısından hello abonelik adı veya kimliği kullanabilirsiniz:

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a>Kaynak grubu oluşturma

Bir kaynak grubu toodeploy IOT hub'ı gerekir. Varolan bir kaynak grubunu kullanın veya yeni bir tane oluşturun.

Aşağıdaki komut toodiscover hello konumlardan nerede IOT hub'ı dağıtabilirsiniz hello kullanabilirsiniz:

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

toocreate IOT Hub, komutu aşağıdaki kullanım hello hello desteklenen konumlardan birinde IOT hub'ınız için bir kaynak grubu. Bu örnek adlı bir kaynak grubu oluşturur **MyIoTRG1** hello içinde **Doğu ABD** bölge:

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a>IoT hub oluşturma

toocreate hello kaynak grubunda hello önceki adımda, komutu aşağıdaki kullanım hello oluşturduğunuz IOT hub'ı. Bu örnekte bir **S1** adlı hub **MyTestIoTHub** hello içinde **Doğu ABD** bölge:

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

hello IOT hub'Hello adı benzersiz olmalıdır.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


Aboneliğinizi komutu aşağıdaki hello kullanarak tüm hello IOT hub'ları listeleyebilirsiniz:

```powershell
Get-AzureRmIotHub
```

Merhaba önceki örnek S1 standart IOT için faturalandırılır hub'ı ekler. Merhaba IOT hub'ı komut aşağıdaki hello kullanarak silebilirsiniz:

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

Alternatif olarak, bir kaynak grubu kaldırabilir ve tüm komut aşağıdaki hello kullanarak içerdiği kaynakların hello:

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a>Sonraki adımlar

PowerShell cmdlet'ini kullanarak bir IOT hub dağıttığınız artık daha fazla tooexplore isteyebilirsiniz:

* Diğer Bul [IOT hub ile çalışmak için PowerShell cmdlet'leri][lnk-iothub-cmdlets].
* Merhaba Hello özellikleri hakkında okuyun [IOT hub'ı kaynak sağlayıcısı REST API][lnk-rest-api].

IOT hub'ı geliştirme hakkında daha fazla toolearn makaleler hello bakın:

* [Giriş tooC SDK][lnk-c-sdk]
* [Azure IOT SDK'ları][lnk-sdks]

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
