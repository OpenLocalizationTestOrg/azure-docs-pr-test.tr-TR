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
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a>Azure Resource Manager şablonu (.NET) kullanılarak IOT hub oluşturma

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Azure Resource Manager toocreate kullanın ve Azure IOT hub'ları program aracılığıyla yönetebilirsiniz. Bu öğretici şunların nasıl yapıldığını gösterir toouse Azure Resource Manager şablonu toocreate IOT hub'ından bir C# programı.

> [!NOTE]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).  Bu makalede, hello Azure Resource Manager dağıtım modeli kullanılarak yer almaktadır.

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Visual Studio 2015 veya Visual Studio 2017.
* Etkin bir Azure hesabı. <br/>Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.
* Bir [Azure depolama hesabı] [ lnk-storage-account] Azure Resource Manager şablonu dosyalarınızı depolayabileceğiniz.
* [Azure PowerShell 1.0] [ lnk-powershell-install] veya sonraki bir sürümü.

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>Visual Studio projenizi hazırlama

1. Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi oluşturma **konsol uygulaması (.NET Framework)** proje şablonu. Ad hello proje **CreateIoTHub**.

2. Çözüm Gezgini'nde, projeye sağ tıklayın ve ardından **NuGet paketlerini Yönet**.

3. NuGet Paket Yöneticisi'nde denetleyin **INCLUDE yayın öncesi**ve hello **Gözat** sayfası Ara **Microsoft.Azure.Management.ResourceManager**. Hello paketi seçin, **yüklemek**, **değişiklikleri gözden** tıklatın **Tamam**, ardından **kabul ediyorum** tooaccept hello lisansları.

4. NuGet Paket Yöneticisi'nde arayın **Microsoft.IdentityModel.Clients.activedirectory tarafından**.  ' I tıklatın **yüklemek**, **değişiklikleri gözden** tıklatın **Tamam**, ardından **kabul ediyorum** tooaccept hello lisans.

5. Program.cs içinde hello varolan **kullanarak** koddan hello ifadelerle:

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. Program.cs içinde statik değişkenler hello yer tutucu değerlerini değiştirerek aşağıdaki hello ekleyin. Not yapılan **ApplicationId**, **Subscriptionıd**, **Tenantıd**, ve **parola** Bu öğreticinin önceki. **Azure depolama hesabınızın adını** hello hello Azure depolama hesabı, Azure Resource Manager şablon dosyalarını depoladığınız adıdır. **Kaynak grubu adı** hello hello IOT hub'ı oluşturduğunuzda kullandığınız hello kaynak grubunun adıdır. Merhaba adı önceden varolan veya yeni bir kaynak grubu olabilir. **Dağıtım adı** hello dağıtımı için bir ad olduğu gibi **Deployment_01**.

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

## <a name="submit-a-template-toocreate-an-iot-hub"></a>Bir şablon toocreate IOT hub'ı gönderme

Kaynak grubunda bir JSON şablonu ve parametre dosyası toocreate IOT hub'ı kullanın. Ayrıca, Azure Resource Manager şablonu toomake değişiklikleri tooan var olan IOT hub'ı kullanabilirsiniz.

1. Çözüm Gezgini'nde, projeye sağ tıklayın, **Ekle**ve ardından **yeni öğe**. Adlı bir JSON dosyası ekleme **template.json** tooyour projesi.

2. Standart bir IOT hub toohello tooadd **Doğu ABD** bölge, Değiştir Merhaba içeriğine **template.json** kaynak tanımı aşağıdaki hello ile. Merhaba geçerli IOT hub'ı destekleyen bölgelerin listesi için bkz: [Azure durumu][lnk-status]:

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

3. Çözüm Gezgini'nde, projeye sağ tıklayın, **Ekle**ve ardından **yeni öğe**. Adlı bir JSON dosyası ekleme **parameters.json** tooyour projesi.

4. Merhaba Değiştir **parameters.json** hello yeni IOT hub için bir ad gibi ayarlar parametre bilgileri aşağıdaki hello ile **{adınızın baş harflerini} mynewiothub**. adı veya baş harfleri içermelidir şekilde hello IOT hub'ı adı genel olarak benzersiz olması gerekir:

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

5. İçinde **Sunucu Gezgini**tooyour Azure aboneliğine bağlanma ve, Azure Storage hesabı oluşturma adlı bir kapsayıcı **şablonları**. Merhaba, **özellikleri** paneli, kümesi hello **herkese okuma erişimi** hello izinlerini **şablonları** kapsayıcı çok**Blob**.

6. İçinde **Sunucu Gezgini**, hello üzerinde sağ **şablonları** kapsayıcı ve ardından **görünüm Blob kapsayıcısını**. Merhaba tıklatın **karşıya Blob** düğmesini tıklatın, hello iki dosyayı seçmeniz **parameters.json** ve **templates.json**ve ardından **açık** tooupload hello JSON dosyaları toohello **şablonları** kapsayıcı. Merhaba JSON verilerini içeren hello BLOB'ları Hello URL'lerini şunlardır:

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. Yöntem tooProgram.cs aşağıdaki hello ekleyin:

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. Aşağıdaki kodu toohello hello eklemek **CreateIoTHub** yöntemi toosubmit hello şablonu ve parametre dosyalarını toohello Azure Resource Manager:

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

9. Aşağıdaki kodu toohello hello eklemek **CreateIoTHub** hello durumunu ve hello yeni IOT hub'ı hello tuşları görüntüler yöntemi:

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a>Tam ve çalışma Merhaba uygulaması

Merhaba uygulaması tarafından arama hello şimdi tamamlayabilirsiniz **CreateIoTHub** oluşturmak ve çalıştırmak için önce yöntemi.

1. Kod toohello hello sonuna aşağıdaki hello eklemek **ana** yöntemi:

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. Tıklatın **yapı** ve ardından **yapı çözümü**. Hataları düzeltin.

3. Tıklatın **hata ayıklama** ve ardından **hata ayıklamayı Başlat** toorun Merhaba uygulaması. Merhaba dağıtım toorun için birkaç dakika sürebilir.

4. Uygulamanızı eklenen tooverify hello yeni IOT hub'ı ziyaret edin hello [Azure portal] [ lnk-azure-portal] ve kaynakları listesini görüntüleyin. Alternatif olarak, hello kullanın **Get-AzureRmResource** PowerShell cmdlet'i.

> [!NOTE]
> Bu örnek uygulama S1 standart IOT için faturalandırılır hub'ı ekler. Merhaba IOT hub'ı hello aracılığıyla silebilirsiniz [Azure portal] [ lnk-azure-portal] veya hello kullanarak **Kaldır AzureRmResource** bitirdiğinizde PowerShell cmdlet'i.

## <a name="next-steps"></a>Sonraki adımlar
Bir C# programı ile bir Azure Resource Manager şablonu kullanarak bir IOT hub dağıttığınız artık daha fazla tooexplore isteyebilirsiniz:

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
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-storage-account]:../storage/common/storage-create-storage-account.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
