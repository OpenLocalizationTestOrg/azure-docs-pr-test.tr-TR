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
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a><span data-ttu-id="4c677-103">C# ve Resource Manager şablonu kullanarak bir Azure sanal makine dağıtma</span><span class="sxs-lookup"><span data-stu-id="4c677-103">Deploy an Azure Virtual Machine using C# and a Resource Manager template</span></span>
<span data-ttu-id="4c677-104">Bu makale size nasıl gösterir toodeploy C# kullanarak Azure Resource Manager şablonu.</span><span class="sxs-lookup"><span data-stu-id="4c677-104">This article shows you how toodeploy an Azure Resource Manager template using C#.</span></span> <span data-ttu-id="4c677-105">oluşturduğunuz hello şablon tek bir alt ağ ile yeni bir sanal ağ içinde Windows Server çalıştıran tek bir sanal makine dağıtır.</span><span class="sxs-lookup"><span data-stu-id="4c677-105">hello template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="4c677-106">Merhaba sanal makine kaynağı ayrıntılı bir açıklaması için bkz: [sanal makineleri bir Azure Resource Manager şablonunda](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="4c677-106">For a detailed description of hello virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="4c677-107">Bir şablona tüm hello kaynaklar hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonu Kılavuzu](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="4c677-107">For more information about all hello resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="4c677-108">Bu adımları toodo yaklaşık 10 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="4c677-108">It takes about 10 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="4c677-109">Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c677-109">Create a Visual Studio project</span></span>

<span data-ttu-id="4c677-110">Bu adımda, Visual Studio yüklü olduğundan ve bir konsol uygulama kullanılan toodeploy hello şablonu oluşturduğunuz emin olun.</span><span class="sxs-lookup"><span data-stu-id="4c677-110">In this step, you make sure that Visual Studio is installed and you create a console application used toodeploy hello template.</span></span>

1. <span data-ttu-id="4c677-111">Henüz yapmadıysanız, yükleme [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="4c677-111">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="4c677-112">Seçin **.NET masaüstü geliştirme** üzerinde iş yükleri sayfa hello ve ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="4c677-112">Select **.NET desktop development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="4c677-113">Hello Özet, görebilirsiniz **.NET Framework 4-4.6 geliştirme araçları** sizin için otomatik olarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="4c677-113">In hello summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="4c677-114">Visual Studio'nun zaten yüklediyseniz, hello .NET iş yükü hello Visual Studio Başlatıcısı kullanarak ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c677-114">If you have already installed Visual Studio, you can add hello .NET workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="4c677-115">Visual Studio'da sırasıyla **dosya** > **yeni** > **proje**.</span><span class="sxs-lookup"><span data-stu-id="4c677-115">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="4c677-116">İçinde **şablonları** > **Visual C#**seçin **konsol uygulaması (.NET Framework)**, girin *myDotnetProject* hello adı için Merhaba proje, select hello hello proje konumunu ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4c677-116">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-hello-packages"></a><span data-ttu-id="4c677-117">Merhaba paket yüklemek için</span><span class="sxs-lookup"><span data-stu-id="4c677-117">Install hello packages</span></span>

<span data-ttu-id="4c677-118">NuGet paketlerini hello kolay şekilde tooinstall hello kitaplıkları adımları toofinish ihtiyacınız var.</span><span class="sxs-lookup"><span data-stu-id="4c677-118">NuGet packages are hello easiest way tooinstall hello libraries that you need toofinish these steps.</span></span> <span data-ttu-id="4c677-119">Visual Studio'da gereksinim tooget hello kitaplıkları adımları yapın:</span><span class="sxs-lookup"><span data-stu-id="4c677-119">tooget hello libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="4c677-120">Tıklatın **Araçları** > **Nuget Paket Yöneticisi**ve ardından **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="4c677-120">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="4c677-121">Merhaba konsolunda aşağıdaki komutları yazın:</span><span class="sxs-lookup"><span data-stu-id="4c677-121">Type these commands in hello console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-hello-files"></a><span data-ttu-id="4c677-122">Merhaba dosyaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c677-122">Create hello files</span></span>

<span data-ttu-id="4c677-123">Bu adımda, hello kaynakları dağıtan bir şablonu ve parametre değerlerini toohello şablon sağlayan bir parametre dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4c677-123">In this step, you create a template file that deploys hello resources and a parameters file that supplies parameter values toohello template.</span></span> <span data-ttu-id="4c677-124">Kullanılan tooperform Azure Resource Manager operations bir yetkilendirme dosya oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="4c677-124">You also create an authorization file that is used tooperform Azure Resource Manager operations.</span></span>

### <a name="create-hello-template-file"></a><span data-ttu-id="4c677-125">Merhaba şablon dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c677-125">Create hello template file</span></span>

1. <span data-ttu-id="4c677-126">Çözüm Gezgini'nde sağ *myDotnetProject* > **Ekle** > **yeni öğe**ve ardından **metin dosyası** içinde *Visual C# öğeleri*.</span><span class="sxs-lookup"><span data-stu-id="4c677-126">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="4c677-127">Ad hello dosyası *CreateVMTemplate.json*ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4c677-127">Name hello file *CreateVMTemplate.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="4c677-128">Oluşturduğunuz bu JSON kod toohello dosyası ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4c677-128">Add this JSON code toohello file that you created:</span></span>

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

3. <span data-ttu-id="4c677-129">Merhaba CreateVMTemplate.json dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4c677-129">Save hello CreateVMTemplate.json file.</span></span>

### <a name="create-hello-parameters-file"></a><span data-ttu-id="4c677-130">Merhaba parametreler dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c677-130">Create hello parameters file</span></span>

<span data-ttu-id="4c677-131">Merhaba şablonunda tanımlanan hello kaynak parametreleri için toospecify değerleri, hello değerleri içeren bir parametre dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4c677-131">toospecify values for hello resource parameters that are defined in hello template, you create a parameters file that contains hello values.</span></span>

1. <span data-ttu-id="4c677-132">Çözüm Gezgini'nde sağ *myDotnetProject* > **Ekle** > **yeni öğe**ve ardından **metin dosyası** içinde *Visual C# öğeleri*.</span><span class="sxs-lookup"><span data-stu-id="4c677-132">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="4c677-133">Ad hello dosyası *Parameters.json*ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4c677-133">Name hello file *Parameters.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="4c677-134">Oluşturduğunuz bu JSON kod toohello dosyası ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4c677-134">Add this JSON code toohello file that you created:</span></span>

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

4. <span data-ttu-id="4c677-135">Merhaba Parameters.json dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4c677-135">Save hello Parameters.json file.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="4c677-136">Merhaba yetkilendirme dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c677-136">Create hello authorization file</span></span>

<span data-ttu-id="4c677-137">Bir şablonu dağıtmadan önce erişim tooan olduğundan emin olun [Active Directory hizmet asıl](../../resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="4c677-137">Before you can deploy a template, make sure that you have access tooan [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span></span> <span data-ttu-id="4c677-138">Hello hizmet sorumlusu istekleri tooAzure Resource Manager kimlik doğrulaması için belirteç alın.</span><span class="sxs-lookup"><span data-stu-id="4c677-138">From hello service principal, you acquire a token for authenticating requests tooAzure Resource Manager.</span></span> <span data-ttu-id="4c677-139">Merhaba uygulama kimliği, hello kimlik doğrulama anahtarı ve hello yetkilendirme dosyasında gereken hello Kiracı kimliği de kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c677-139">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in hello authorization file.</span></span>

1. <span data-ttu-id="4c677-140">Çözüm Gezgini'nde sağ *myDotnetProject* > **Ekle** > **yeni öğe**ve ardından **metin dosyası** içinde *Visual C# öğeleri*.</span><span class="sxs-lookup"><span data-stu-id="4c677-140">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="4c677-141">Ad hello dosyası *azureauth.properties*ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="4c677-141">Name hello file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="4c677-142">Bu yetkilendirme özellikleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4c677-142">Add these authorization properties:</span></span>

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

    <span data-ttu-id="4c677-143">Değiştir  **&lt;abonelik kimliği&gt;**  , abonelik tanımlayıcısı ile  **&lt;uygulama kimliği&gt;**  hello Active Directory uygulaması ile tanımlayıcı,  **&lt;kimlik doğrulama anahtarı&gt;**  hello uygulama anahtarla ve  **&lt;Kiracı kimliği&gt;**  hello Kiracı tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="4c677-143">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

3. <span data-ttu-id="4c677-144">Merhaba azureauth.properties dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4c677-144">Save hello azureauth.properties file.</span></span>
4. <span data-ttu-id="4c677-145">Windows ortam değişkeninde AZURE_AUTH_LOCATION, oluşturduğunuz hello tam yolu tooauthorization dosya ile adlandırılmış kümesi örneğin hello aşağıdaki PowerShell komutu kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="4c677-145">Set an environment variable in Windows named AZURE_AUTH_LOCATION with hello full path tooauthorization file that you created, for example hello following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-hello-management-client"></a><span data-ttu-id="4c677-146">Merhaba yönetim istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c677-146">Create hello management client</span></span>

1. <span data-ttu-id="4c677-147">Oluşturduğunuz hello projesi için Hello Program.cs dosyasını açın ve bunlar hello dosyasının üst kısmında using deyimleri toohello varolan deyimleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4c677-147">Open hello Program.cs file for hello project that you created, and then add these using statements toohello existing statements at top of hello file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

2. <span data-ttu-id="4c677-148">toocreate hello yönetim istemcisi, bu kod toohello Main yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4c677-148">toocreate hello management client, add this code toohello Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="4c677-149">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c677-149">Create a resource group</span></span>

<span data-ttu-id="4c677-150">toospecify değerleri Merhaba uygulaması için kod toohello Main yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4c677-150">toospecify values for hello application, add code toohello Main method:</span></span>

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a><span data-ttu-id="4c677-151">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c677-151">Create a storage account</span></span>

<span data-ttu-id="4c677-152">Azure depolama hesabından Hello şablonu ve parametre dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="4c677-152">hello template and parameters are deployed from a storage account in Azure.</span></span> <span data-ttu-id="4c677-153">Bu adımda, hello hesabı oluşturun ve hello dosyaları karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="4c677-153">In this step, you create hello account and upload hello files.</span></span> 

<span data-ttu-id="4c677-154">toocreate Merhaba hesabı, bu kod toohello Main yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4c677-154">toocreate hello account, add this code toohello Main method:</span></span>

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

## <a name="deploy-hello-template"></a><span data-ttu-id="4c677-155">Merhaba şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="4c677-155">Deploy hello template</span></span>

<span data-ttu-id="4c677-156">Merhaba şablonu ve oluşturulan hello depolama hesabı parametrelerinden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="4c677-156">Deploy hello template and parameters from hello storage account that was created.</span></span> 

<span data-ttu-id="4c677-157">toodeploy hello şablonu, bu kod toohello Main yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4c677-157">toodeploy hello template, add this code toohello Main method:</span></span>

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

## <a name="delete-hello-resources"></a><span data-ttu-id="4c677-158">Merhaba kaynakları silin</span><span class="sxs-lookup"><span data-stu-id="4c677-158">Delete hello resources</span></span>

<span data-ttu-id="4c677-159">Azure'da kullanılan kaynaklar için ücretlendirildiğinizden, her zaman artık gerekli olmayan iyi bir uygulama toodelete kaynaklarını aşıyor.</span><span class="sxs-lookup"><span data-stu-id="4c677-159">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="4c677-160">Bir kaynak grubundan ayrı ayrı her bir kaynağın toodelete gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="4c677-160">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="4c677-161">Delete hello kaynak grubunu ve tüm kaynakları otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="4c677-161">Delete hello resource group and all its resources are automatically deleted.</span></span> 

<span data-ttu-id="4c677-162">toodelete hello kaynak grubu, bu kod toohello Main yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4c677-162">toodelete hello resource group, add this code toohello Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a><span data-ttu-id="4c677-163">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="4c677-163">Run hello application</span></span>

<span data-ttu-id="4c677-164">Bu konsol uygulaması toorun başlangıç toofinish itibaren tümüyle yaklaşık beş dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="4c677-164">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> 

1. <span data-ttu-id="4c677-165">toorun hello konsol uygulaması tıklatın **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="4c677-165">toorun hello console application, click **Start**.</span></span>

2. <span data-ttu-id="4c677-166">Tuşuna önce **Enter** toostart silme kaynakları, birkaç dakika sürebilir hello kaynak tooverify hello oluşturmayı hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="4c677-166">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="4c677-167">Merhaba dağıtım durumu toosee hello dağıtım bilgilerini'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4c677-167">Click hello deployment status toosee information about hello deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c677-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4c677-168">Next steps</span></span>
* <span data-ttu-id="4c677-169">Hello dağıtımı ile ilgili sorunlar varsa, bir sonraki adım, toolook olacaktır [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="4c677-169">If there were issues with hello deployment, a next step would be toolook at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="4c677-170">Bilgi nasıl toodeploy bir sanal makine ve destekleyici kaynaklarıyla inceleyerek [bir Azure sanal makine kullanarak C# dağıtmak](csharp.md).</span><span class="sxs-lookup"><span data-stu-id="4c677-170">Learn how toodeploy a virtual machine and its supporting resources by reviewing [Deploy an Azure Virtual Machine Using C#](csharp.md).</span></span>
