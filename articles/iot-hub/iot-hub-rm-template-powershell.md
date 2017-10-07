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
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a>Azure Resource Manager şablonu (PowerShell) kullanarak IOT hub oluşturma

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Azure Resource Manager toocreate kullanın ve Azure IOT hub'ları program aracılığıyla yönetebilirsiniz. Bu öğretici şunların nasıl yapıldığını gösterir toouse Azure Resource Manager şablonu toocreate PowerShell ile bir IOT hub.

> [!NOTE]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Azure Resource Manager dağıtım modeli kullanılarak yer almaktadır.

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Etkin bir Azure hesabı. <br/>Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.
* [Azure PowerShell 1.0] [ lnk-powershell-install] veya sonraki bir sürümü.

> [!TIP]
> Merhaba makale [Azure PowerShell kullanarak Azure Resource Manager ile] [ lnk-powershell-arm] hakkında daha fazla bilgi sağlayan toouse PowerShell ve Azure Resource Manager şablonları toocreate Azure kaynakları.

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

Burada bir IOT hub'ı dağıtabilir ve şu anda desteklenen API sürümleri hello komutları toodiscover aşağıdaki hello kullanabilirsiniz:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

Bir kaynak grubu toocontain komutu IOT hub'ına yönelik hello desteklenen konumlardan birinde aşağıdaki hello kullanarak IOT hub'ınızı oluşturun. Bu örnek adlı bir kaynak grubu oluşturur **MyIoTRG1**:

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a>Bir şablon toocreate IOT hub'ı gönderme

Kaynak grubunda bir JSON şablonu toocreate IOT hub'ı kullanın. Ayrıca, Azure Resource Manager şablonu toomake değişiklikleri tooan var olan IOT hub'ı kullanabilirsiniz.

1. Bir Azure Resource Manager şablonu olarak adlandırılan bir metin düzenleyicisi toocreate kullanmak **template.json** ile yeni bir standart IOT hub kaynak tanımı toocreate hello. Bu örnek, hello hello IOT hub'ı ekler **Doğu ABD** bölge, iki tüketici grupları oluşturur (**cg1** ve **cg2**) hello Event Hub ile uyumlu uç nokta ve kullandığı hello **2016-02-03** API sürümü. Bu şablon Ayrıca, toopass hello IOT hub adı adlı bir parametre olarak bekliyor **hubName**. Merhaba geçerli IOT hub'ı destekleyen konumların listesini için görmek [Azure durumu][lnk-status].

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

2. Yerel makinenizde Hello Azure Resource Manager şablonu dosyasını kaydedin. Bu örnek kaydettiğiniz bu adlı bir klasöre varsayar **c:\templates**.

3. Komut toodeploy aşağıdaki hello IOT hub'ınızı hello adını parametre olarak geçirme, yeni IOT hub ' ınızı çalıştırın. Bu örnekte, hello hello IOT hub'ı adıdır `abcmyiothub`. IOT hub'ınızı Hello adı genel olarak benzersiz olması gerekir:

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. Merhaba çıktı hello tuşları oluşturduğunuz hello IOT hub'ı görüntüler.

5. Uygulamanızı eklenen tooverify hello yeni IOT hub'ı ziyaret edin hello [Azure portal] [ lnk-azure-portal] ve kaynakları listesini görüntüleyin. Alternatif olarak, hello kullanın **Get-AzureRmResource** PowerShell cmdlet'i.

> [!NOTE]
> Bu örnek uygulama S1 standart IOT için faturalandırılır hub'ı ekler. Merhaba IOT hub'ı hello aracılığıyla silebilirsiniz [Azure portal] [ lnk-azure-portal] veya hello kullanarak **Kaldır AzureRmResource** bitirdiğinizde PowerShell cmdlet'i.

## <a name="next-steps"></a>Sonraki adımlar

PowerShell ile bir Azure Resource Manager şablonu kullanarak bir IOT hub dağıttığınız artık daha fazla tooexplore isteyebilirsiniz:

* Merhaba Hello özellikleri hakkında okuyun [IOT hub'ı kaynak sağlayıcısı REST API][lnk-rest-api].
* Okuma [Azure Resource Manager'a genel bakış] [ lnk-azure-rm-overview] toolearn hello özellikleri Azure Kaynak Yöneticisi'nin hakkında daha fazla.

IOT hub'ı geliştirme hakkında daha fazla toolearn makaleler hello bakın:

* [Giriş tooC SDK][lnk-c-sdk]
* [Azure IOT SDK'ları][lnk-sdks]

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]

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
