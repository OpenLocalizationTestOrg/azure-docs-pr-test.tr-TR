---
title: "C# ve Resource Manager şablonu kullanarak VM bir aaaDeploy | Microsoft Docs"
description: "Toohow toouse C# ve Resource Manager şablonu toodeploy bir Azure VM öğrenin."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: bfba66e8-c923-4df2-900a-0c2643b81240
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: davidmu
ms.openlocfilehash: 91d470228cfeed72336b488ffef4dfbb25bc3a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a>C# ve Resource Manager şablonu kullanarak bir Azure sanal makine dağıtma
Bu makale size nasıl gösterir toodeploy C# kullanarak Azure Resource Manager şablonu. oluşturduğunuz hello şablon tek bir alt ağ ile yeni bir sanal ağ içinde Windows Server çalıştıran tek bir sanal makine dağıtır.

Merhaba sanal makine kaynağı ayrıntılı bir açıklaması için bkz: [sanal makineleri bir Azure Resource Manager şablonunda](template-description.md). Bir şablona tüm hello kaynaklar hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonu Kılavuzu](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Bu adımları toodo yaklaşık 10 dakika sürer.

## <a name="create-a-visual-studio-project"></a>Visual Studio projesi oluşturma

Bu adımda, Visual Studio yüklü olduğundan ve bir konsol uygulama kullanılan toodeploy hello şablonu oluşturduğunuz emin olun.

1. Henüz yapmadıysanız, yükleme [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Seçin **.NET masaüstü geliştirme** üzerinde iş yükleri sayfa hello ve ardından **yükleme**. Hello Özet, görebilirsiniz **.NET Framework 4-4.6 geliştirme araçları** sizin için otomatik olarak seçilir. Visual Studio'nun zaten yüklediyseniz, hello .NET iş yükü hello Visual Studio Başlatıcısı kullanarak ekleyebilirsiniz.
2. Visual Studio'da sırasıyla **dosya** > **yeni** > **proje**.
3. İçinde **şablonları** > **Visual C#**seçin **konsol uygulaması (.NET Framework)**, girin *myDotnetProject* hello adı için Merhaba proje, select hello hello proje konumunu ve ardından **Tamam**.

## <a name="install-hello-packages"></a>Merhaba paket yüklemek için

NuGet paketlerini hello kolay şekilde tooinstall hello kitaplıkları adımları toofinish ihtiyacınız var. Visual Studio'da gereksinim tooget hello kitaplıkları adımları yapın:

1. Tıklatın **Araçları** > **Nuget Paket Yöneticisi**ve ardından **Paket Yöneticisi Konsolu**.
2. Merhaba konsolunda aşağıdaki komutları yazın:

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-hello-files"></a>Merhaba dosyaları oluşturma

Bu adımda, hello kaynakları dağıtan bir şablonu ve parametre değerlerini toohello şablon sağlayan bir parametre dosyası oluşturun. Kullanılan tooperform Azure Resource Manager operations bir yetkilendirme dosya oluşturabilir.

### <a name="create-hello-template-file"></a>Merhaba şablon dosyası oluşturma

1. Çözüm Gezgini'nde sağ *myDotnetProject* > **Ekle** > **yeni öğe**ve ardından **metin dosyası** içinde *Visual C# öğeleri*. Ad hello dosyası *CreateVMTemplate.json*ve ardından **Ekle**.
2. Oluşturduğunuz bu JSON kod toohello dosyası ekleyin:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

3. Merhaba CreateVMTemplate.json dosyasını kaydedin.

### <a name="create-hello-parameters-file"></a>Merhaba parametreler dosyası oluşturma

Merhaba şablonunda tanımlanan hello kaynak parametreleri için toospecify değerleri, hello değerleri içeren bir parametre dosyası oluşturun.

1. Çözüm Gezgini'nde sağ *myDotnetProject* > **Ekle** > **yeni öğe**ve ardından **metin dosyası** içinde *Visual C# öğeleri*. Ad hello dosyası *Parameters.json*ve ardından **Ekle**.
2. Oluşturduğunuz bu JSON kod toohello dosyası ekleyin:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

4. Merhaba Parameters.json dosyasını kaydedin.

### <a name="create-hello-authorization-file"></a>Merhaba yetkilendirme dosyası oluşturma

Bir şablonu dağıtmadan önce erişim tooan olduğundan emin olun [Active Directory hizmet asıl](../../resource-group-authenticate-service-principal.md). Hello hizmet sorumlusu istekleri tooAzure Resource Manager kimlik doğrulaması için belirteç alın. Merhaba uygulama kimliği, hello kimlik doğrulama anahtarı ve hello yetkilendirme dosyasında gereken hello Kiracı kimliği de kaydetmeniz gerekir.

1. Çözüm Gezgini'nde sağ *myDotnetProject* > **Ekle** > **yeni öğe**ve ardından **metin dosyası** içinde *Visual C# öğeleri*. Ad hello dosyası *azureauth.properties*ve ardından **Ekle**.
2. Bu yetkilendirme özellikleri ekleyin:

    ```
    subscription=<subscription-id>
    client=<application-id>
    key=<authentication-key>
    tenant=<tenant-id>
    managementURI=https://management.core.windows.net/
    baseURL=https://management.azure.com/
    authURL=https://login.windows.net/
    graphURL=https://graph.windows.net/
    ```

    Değiştir  **&lt;abonelik kimliği&gt;**  , abonelik tanımlayıcısı ile  **&lt;uygulama kimliği&gt;**  hello Active Directory uygulaması ile tanımlayıcı,  **&lt;kimlik doğrulama anahtarı&gt;**  hello uygulama anahtarla ve  **&lt;Kiracı kimliği&gt;**  hello Kiracı tanımlayıcı.

3. Merhaba azureauth.properties dosyasını kaydedin.
4. Windows ortam değişkeninde AZURE_AUTH_LOCATION, oluşturduğunuz hello tam yolu tooauthorization dosya ile adlandırılmış kümesi örneğin hello aşağıdaki PowerShell komutu kullanılabilir:

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-hello-management-client"></a>Merhaba yönetim istemcisi oluşturma

1. Oluşturduğunuz hello projesi için Hello Program.cs dosyasını açın ve bunlar hello dosyasının üst kısmında using deyimleri toohello varolan deyimleri ekleyin:

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

2. toocreate hello yönetim istemcisi, bu kod toohello Main yöntemi ekleyin:

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

toospecify değerleri Merhaba uygulaması için kod toohello Main yöntemi ekleyin:

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a>Depolama hesabı oluşturma

Azure depolama hesabından Hello şablonu ve parametre dağıtılır. Bu adımda, hello hesabı oluşturun ve hello dosyaları karşıya yükleme. 

toocreate Merhaba hesabı, bu kod toohello Main yöntemi ekleyin:

```
string storageAccountName = SdkContext.RandomResourceName("st", 10);

Console.WriteLine("Creating storage account...");
var storage = azure.StorageAccounts.Define(storageAccountName)
    .WithRegion(Region.USWest)
    .WithExistingResourceGroup(resourceGroup)
    .Create();

var storageKeys = storage.GetKeys();
string storageConnectionString = "DefaultEndpointsProtocol=https;"
    + "AccountName=" + storage.Name
    + ";AccountKey=" + storageKeys[0].Value
    + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
var serviceClient = account.CreateCloudBlobClient();

Console.WriteLine("Creating container...");
var container = serviceClient.GetContainerReference("templates");
container.CreateIfNotExistsAsync().Wait();
var containerPermissions = new BlobContainerPermissions()
    { PublicAccess = BlobContainerPublicAccessType.Container };
container.SetPermissionsAsync(containerPermissions).Wait();

Console.WriteLine("Uploading template file...");
var templateblob = container.GetBlockBlobReference("CreateVMTemplate.json");
templateblob.UploadFromFile("..\\..\\CreateVMTemplate.json");

Console.WriteLine("Uploading parameters file...");
var paramblob = container.GetBlockBlobReference("Parameters.json");
paramblob.UploadFromFile("..\\..\\Parameters.json");
```

## <a name="deploy-hello-template"></a>Merhaba şablonu dağıtma

Merhaba şablonu ve oluşturulan hello depolama hesabı parametrelerinden dağıtın. 

toodeploy hello şablonu, bu kod toohello Main yöntemi ekleyin:

```
var templatePath = "https://" + storageAccountName + ".blob.core.windows.net/templates/CreateVMTemplate.json";
var paramPath = "https://" + storageAccountName + ".blob.core.windows.net/templates/Parameters.json";
var deployment = azure.Deployments.Define("myDeployment")
    .WithExistingResourceGroup(groupName)
    .WithTemplateLink(templatePath, "1.0.0.0")
    .WithParametersLink(paramPath, "1.0.0.0")
    .WithMode(Microsoft.Azure.Management.ResourceManager.Fluent.Models.DeploymentMode.Incremental)
    .Create();
Console.WriteLine("Press enter toodelete hello resource group...");
Console.ReadLine();
```

## <a name="delete-hello-resources"></a>Merhaba kaynakları silin

Azure'da kullanılan kaynaklar için ücretlendirildiğinizden, her zaman artık gerekli olmayan iyi bir uygulama toodelete kaynaklarını aşıyor. Bir kaynak grubundan ayrı ayrı her bir kaynağın toodelete gerek yoktur. Delete hello kaynak grubunu ve tüm kaynakları otomatik olarak silinir. 

toodelete hello kaynak grubu, bu kod toohello Main yöntemi ekleyin:

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın

Bu konsol uygulaması toorun başlangıç toofinish itibaren tümüyle yaklaşık beş dakika sürer. 

1. toorun hello konsol uygulaması tıklatın **Başlat**.

2. Tuşuna önce **Enter** toostart silme kaynakları, birkaç dakika sürebilir hello kaynak tooverify hello oluşturmayı hello Azure portalı. Merhaba dağıtım durumu toosee hello dağıtım bilgilerini'ı tıklatın.

## <a name="next-steps"></a>Sonraki adımlar
* Hello dağıtımı ile ilgili sorunlar varsa, bir sonraki adım, toolook olacaktır [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](../../resource-manager-common-deployment-errors.md).
* Bilgi nasıl toodeploy bir sanal makine ve destekleyici kaynaklarıyla inceleyerek [bir Azure sanal makine kullanarak C# dağıtmak](csharp.md).
