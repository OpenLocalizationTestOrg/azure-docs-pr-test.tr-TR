---
title: "C# ve Resource Manager şablonu kullanarak bir VM'i dağıtma | Microsoft Docs"
description: "Bir Azure VM dağıtmak için C# ve Resource Manager şablonu kullanmak için öğrenin."
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
ms.openlocfilehash: bd1c860db026f948202cd1f3aa763b4547c597b4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a><span data-ttu-id="dbd8b-103">C# ve Resource Manager şablonu kullanarak bir Azure sanal makine dağıtma</span><span class="sxs-lookup"><span data-stu-id="dbd8b-103">Deploy an Azure Virtual Machine using C# and a Resource Manager template</span></span>
<span data-ttu-id="dbd8b-104">Bu makalede, C# kullanarak Azure Resource Manager şablonu dağıtma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-104">This article shows you how to deploy an Azure Resource Manager template using C#.</span></span> <span data-ttu-id="dbd8b-105">Oluşturduğunuz şablon, tek bir alt ağ ile yeni bir sanal ağ içinde Windows Server çalıştıran tek bir sanal makine dağıtır.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-105">The template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="dbd8b-106">Sanal makine kaynağı ayrıntılı bir açıklaması için bkz: [sanal makineleri bir Azure Resource Manager şablonunda](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="dbd8b-106">For a detailed description of the virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="dbd8b-107">Bir şablona tüm kaynaklar hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonu Kılavuzu](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="dbd8b-107">For more information about all the resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="dbd8b-108">Bu adımları yapmak için yaklaşık 10 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-108">It takes about 10 minutes to do these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="dbd8b-109">Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="dbd8b-109">Create a Visual Studio project</span></span>

<span data-ttu-id="dbd8b-110">Bu adımda, Visual Studio yüklenmiş ve şablonu dağıtmak için kullanılan bir konsol uygulaması oluşturun emin olun.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-110">In this step, you make sure that Visual Studio is installed and you create a console application used to deploy the template.</span></span>

1. <span data-ttu-id="dbd8b-111">Henüz yapmadıysanız, yükleme [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="dbd8b-111">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="dbd8b-112">Seçin **.NET masaüstü geliştirme** iş yükleri sayfa ve ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-112">Select **.NET desktop development** on the Workloads page, and then click **Install**.</span></span> <span data-ttu-id="dbd8b-113">Özet olarak, gördüğünüz **.NET Framework 4-4.6 geliştirme araçları** sizin için otomatik olarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-113">In the summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="dbd8b-114">Visual Studio'nun zaten yüklediyseniz, Visual Studio Başlatıcısı'nı kullanarak .NET iş yükü ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-114">If you have already installed Visual Studio, you can add the .NET workload using the Visual Studio Launcher.</span></span>
2. <span data-ttu-id="dbd8b-115">Visual Studio'da sırasıyla **dosya** > **yeni** > **proje**.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-115">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="dbd8b-116">İçinde **şablonları** > **Visual C#**seçin **konsol uygulaması (.NET Framework)**, girin *myDotnetProject* projesinin adı, proje konumunu seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-116">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for the name of the project, select the location of the project, and then click **OK**.</span></span>

## <a name="install-the-packages"></a><span data-ttu-id="dbd8b-117">Paket yüklemek için</span><span class="sxs-lookup"><span data-stu-id="dbd8b-117">Install the packages</span></span>

<span data-ttu-id="dbd8b-118">NuGet paketleri, bu adımları tamamlamak için gereken kitaplıklar yüklemek için kolay bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-118">NuGet packages are the easiest way to install the libraries that you need to finish these steps.</span></span> <span data-ttu-id="dbd8b-119">Visual Studio'da ihtiyacınız kitaplıkları almak için bu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="dbd8b-119">To get the libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="dbd8b-120">Tıklatın **Araçları** > **Nuget Paket Yöneticisi**ve ardından **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-120">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="dbd8b-121">Konsolunda aşağıdaki komutları yazın:</span><span class="sxs-lookup"><span data-stu-id="dbd8b-121">Type these commands in the console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-the-files"></a><span data-ttu-id="dbd8b-122">Dosyaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="dbd8b-122">Create the files</span></span>

<span data-ttu-id="dbd8b-123">Bu adımda, kaynakları dağıtan bir şablon dosyası ve şablon parametre değerlerini sağlayan bir parametre dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-123">In this step, you create a template file that deploys the resources and a parameters file that supplies parameter values to the template.</span></span> <span data-ttu-id="dbd8b-124">Ayrıca Azure Resource Manager işlemlerini gerçekleştirmek için kullanılan bir yetkilendirme dosyasını oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-124">You also create an authorization file that is used to perform Azure Resource Manager operations.</span></span>

### <a name="create-the-template-file"></a><span data-ttu-id="dbd8b-125">Şablon dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="dbd8b-125">Create the template file</span></span>

1. <span data-ttu-id="dbd8b-126">Çözüm Gezgini'nde sağ *myDotnetProject* > **Ekle** > **yeni öğe**ve ardından **metin dosyası** içinde *Visual C# öğeleri*.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-126">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="dbd8b-127">Dosya adı *CreateVMTemplate.json*ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-127">Name the file *CreateVMTemplate.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="dbd8b-128">Bu JSON kodunu oluşturduğunuz dosyaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="dbd8b-128">Add this JSON code to the file that you created:</span></span>

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

3. <span data-ttu-id="dbd8b-129">CreateVMTemplate.json dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-129">Save the CreateVMTemplate.json file.</span></span>

### <a name="create-the-parameters-file"></a><span data-ttu-id="dbd8b-130">Parametreler dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="dbd8b-130">Create the parameters file</span></span>

<span data-ttu-id="dbd8b-131">Şablonda tanımlı kaynak parametreleri için değerleri belirtmek için değerleri içeren bir parametre dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-131">To specify values for the resource parameters that are defined in the template, you create a parameters file that contains the values.</span></span>

1. <span data-ttu-id="dbd8b-132">Çözüm Gezgini'nde sağ *myDotnetProject* > **Ekle** > **yeni öğe**ve ardından **metin dosyası** içinde *Visual C# öğeleri*.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-132">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="dbd8b-133">Dosya adı *Parameters.json*ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-133">Name the file *Parameters.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="dbd8b-134">Bu JSON kodunu oluşturduğunuz dosyaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="dbd8b-134">Add this JSON code to the file that you created:</span></span>

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

4. <span data-ttu-id="dbd8b-135">Parameters.json dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-135">Save the Parameters.json file.</span></span>

### <a name="create-the-authorization-file"></a><span data-ttu-id="dbd8b-136">Yetkilendirme dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="dbd8b-136">Create the authorization file</span></span>

<span data-ttu-id="dbd8b-137">Bir şablonu dağıtmadan önce erişimi olduğundan emin olun bir [Active Directory hizmet asıl](../../resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="dbd8b-137">Before you can deploy a template, make sure that you have access to an [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span></span> <span data-ttu-id="dbd8b-138">Hizmet sorumlusu istekleri için Azure Resource Manager kimlik doğrulaması için belirteç alın.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-138">From the service principal, you acquire a token for authenticating requests to Azure Resource Manager.</span></span> <span data-ttu-id="dbd8b-139">Uygulama kimliği, kimlik doğrulama anahtarı ve yetkilendirme dosyasında gereken Kiracı kimliği de kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-139">You should also record the application ID, the authentication key, and the tenant ID that you need in the authorization file.</span></span>

1. <span data-ttu-id="dbd8b-140">Çözüm Gezgini'nde sağ *myDotnetProject* > **Ekle** > **yeni öğe**ve ardından **metin dosyası** içinde *Visual C# öğeleri*.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-140">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="dbd8b-141">Dosya adı *azureauth.properties*ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-141">Name the file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="dbd8b-142">Bu yetkilendirme özellikleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="dbd8b-142">Add these authorization properties:</span></span>

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

    <span data-ttu-id="dbd8b-143">Değiştir  **&lt;abonelik kimliği&gt;**  , abonelik tanımlayıcısı ile  **&lt;uygulama kimliği&gt;**  Active Directory Uygulama tanımlayıcısı ile  **&lt;kimlik doğrulama anahtarı&gt;**  uygulama anahtarla ve  **&lt;Kiracı kimliği&gt;**  , Kiracı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-143">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with the Active Directory application identifier, **&lt;authentication-key&gt;** with the application key, and **&lt;tenant-id&gt;** with the tenant identifier.</span></span>

3. <span data-ttu-id="dbd8b-144">Azureauth.properties dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-144">Save the azureauth.properties file.</span></span>
4. <span data-ttu-id="dbd8b-145">Windows, oluşturduğunuz örneğin komut kullanılabilir aşağıdaki PowerShell yetkilendirme dosyasının tam yolunu AZURE_AUTH_LOCATION adında bir ortam değişkeni ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="dbd8b-145">Set an environment variable in Windows named AZURE_AUTH_LOCATION with the full path to authorization file that you created, for example the following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-the-management-client"></a><span data-ttu-id="dbd8b-146">Yönetim istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="dbd8b-146">Create the management client</span></span>

1. <span data-ttu-id="dbd8b-147">Oluşturduğunuz proje için Program.cs dosyasını açın ve bu dosyanın üst kısmında using deyimleri varolan deyimleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="dbd8b-147">Open the Program.cs file for the project that you created, and then add these using statements to the existing statements at top of the file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

2. <span data-ttu-id="dbd8b-148">Yönetim istemcisi oluşturmak için bu kodu Main yöntemine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="dbd8b-148">To create the management client, add this code to the Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="dbd8b-149">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="dbd8b-149">Create a resource group</span></span>

<span data-ttu-id="dbd8b-150">Uygulama için değerleri belirtmek için kodu Main yöntemine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="dbd8b-150">To specify values for the application, add code to the Main method:</span></span>

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a><span data-ttu-id="dbd8b-151">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dbd8b-151">Create a storage account</span></span>

<span data-ttu-id="dbd8b-152">Azure depolama hesabından şablonu ve parametre dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-152">The template and parameters are deployed from a storage account in Azure.</span></span> <span data-ttu-id="dbd8b-153">Bu adımda, hesabı oluşturun ve dosyaları karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-153">In this step, you create the account and upload the files.</span></span> 

<span data-ttu-id="dbd8b-154">Hesabı oluşturmak için bu kodu Main yöntemine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="dbd8b-154">To create the account, add this code to the Main method:</span></span>

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

## <a name="deploy-the-template"></a><span data-ttu-id="dbd8b-155">Şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="dbd8b-155">Deploy the template</span></span>

<span data-ttu-id="dbd8b-156">Şablon ve oluşturulan depolama hesabı parametrelerinden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-156">Deploy the template and parameters from the storage account that was created.</span></span> 

<span data-ttu-id="dbd8b-157">Şablonu dağıtmak için bu kodu Main yöntemine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="dbd8b-157">To deploy the template, add this code to the Main method:</span></span>

```
var templatePath = "https://" + storageAccountName + ".blob.core.windows.net/templates/CreateVMTemplate.json";
var paramPath = "https://" + storageAccountName + ".blob.core.windows.net/templates/Parameters.json";
var deployment = azure.Deployments.Define("myDeployment")
    .WithExistingResourceGroup(groupName)
    .WithTemplateLink(templatePath, "1.0.0.0")
    .WithParametersLink(paramPath, "1.0.0.0")
    .WithMode(Microsoft.Azure.Management.ResourceManager.Fluent.Models.DeploymentMode.Incremental)
    .Create();
Console.WriteLine("Press enter to delete the resource group...");
Console.ReadLine();
```

## <a name="delete-the-resources"></a><span data-ttu-id="dbd8b-158">Kaynakları silme</span><span class="sxs-lookup"><span data-stu-id="dbd8b-158">Delete the resources</span></span>

<span data-ttu-id="dbd8b-159">Azure'da kullanılan kaynaklar için ücretlendirildiğinizden, her zaman artık gerekli olmayan kaynakları silmek için iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-159">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="dbd8b-160">Her kaynak ayrı ayrı bir kaynak grubundan silmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-160">You don’t need to delete each resource separately from a resource group.</span></span> <span data-ttu-id="dbd8b-161">Kaynak grubunu silin ve tüm kaynakları otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-161">Delete the resource group and all its resources are automatically deleted.</span></span> 

<span data-ttu-id="dbd8b-162">Kaynak grubunu silmek için bu kodu Main yöntemine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="dbd8b-162">To delete the resource group, add this code to the Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-the-application"></a><span data-ttu-id="dbd8b-163">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="dbd8b-163">Run the application</span></span>

<span data-ttu-id="dbd8b-164">Tamamlamak için bu konsol uygulamasını tamamen çalıştırın yaklaşık beş dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-164">It should take about five minutes for this console application to run completely from start to finish.</span></span> 

1. <span data-ttu-id="dbd8b-165">Konsol uygulamasını çalıştırmak için tıklatın **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-165">To run the console application, click **Start**.</span></span>

2. <span data-ttu-id="dbd8b-166">Tuşuna önce **Enter** kaynakları silme başlatmak için Azure portalında kaynakların oluşturulmasını doğrulamak için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-166">Before you press **Enter** to start deleting resources, you could take a few minutes to verify the creation of the resources in the Azure portal.</span></span> <span data-ttu-id="dbd8b-167">Dağıtım hakkında bilgi için dağıtım durumunu tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dbd8b-167">Click the deployment status to see information about the deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dbd8b-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dbd8b-168">Next steps</span></span>
* <span data-ttu-id="dbd8b-169">Dağıtım ile ilgili sorunlar varsa, bir sonraki adım bakmak için olacaktır [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="dbd8b-169">If there were issues with the deployment, a next step would be to look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="dbd8b-170">Bir sanal makine ve destekleyici kaynaklarıyla gözden geçirerek dağıtmayı öğrenin [bir Azure sanal makine kullanarak C# dağıtmak](csharp.md).</span><span class="sxs-lookup"><span data-stu-id="dbd8b-170">Learn how to deploy a virtual machine and its supporting resources by reviewing [Deploy an Azure Virtual Machine Using C#](csharp.md).</span></span>
