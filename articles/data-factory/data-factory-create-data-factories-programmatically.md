---
title: "Azure .NET SDK kullanarak aaaCreate veri ardışık | Microsoft Docs"
description: "Nasıl tooprogrammatically oluşturmak, izlemek ve Data Factory SDK'yı kullanarak Azure data factory'leri yönetmek öğrenin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="75354-103">Oluşturma, izlemek ve Azure Data Factory .NET SDK kullanarak Azure data factory'leri yönetme</span><span class="sxs-lookup"><span data-stu-id="75354-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="75354-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="75354-104">Overview</span></span>
<span data-ttu-id="75354-105">Oluşturun, izlemek ve program aracılığıyla Data Factory .NET SDK kullanarak Azure data factory'leri yönetin.</span><span class="sxs-lookup"><span data-stu-id="75354-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="75354-106">Bu makalede toocreate oluşturan ve veri fabrikası izler örnek bir .NET konsol uygulaması izleyebileceğiniz bir kılavuz içerir.</span><span class="sxs-lookup"><span data-stu-id="75354-106">This article contains a walkthrough that you can follow toocreate a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="75354-107">Bu makalede, tüm hello veri fabrikası .NET API kapsamaz.</span><span class="sxs-lookup"><span data-stu-id="75354-107">This article does not cover all hello Data Factory .NET API.</span></span> <span data-ttu-id="75354-108">Bkz: [Data Factory .NET API Başvurusu](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) hakkında kapsamlı bilgi için .NET API veri fabrikası için.</span><span class="sxs-lookup"><span data-stu-id="75354-108">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="75354-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="75354-109">Prerequisites</span></span>
* <span data-ttu-id="75354-110">Visual Studio 2012 veya 2013 veya 2015</span><span class="sxs-lookup"><span data-stu-id="75354-110">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="75354-111">İndirme ve yükleme [Azure .NET SDK'sı](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="75354-111">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="75354-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="75354-112">Azure PowerShell.</span></span> <span data-ttu-id="75354-113">' Ndaki yönergeleri izleyin [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) tooinstall Azure PowerShell, bilgisayarınızda makalesi.</span><span class="sxs-lookup"><span data-stu-id="75354-113">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="75354-114">Azure PowerShell toocreate bir Azure Active Directory uygulamasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="75354-114">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="75354-115">Azure Active Directory’de uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="75354-115">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="75354-116">Bir Azure Active Directory uygulaması oluşturmak, Merhaba uygulaması için bir hizmet sorumlusu oluşturmak ve toohello atamak **veri fabrikası katkıda bulunan** rol.</span><span class="sxs-lookup"><span data-stu-id="75354-116">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="75354-117">**PowerShell**’i başlatın.</span><span class="sxs-lookup"><span data-stu-id="75354-117">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="75354-118">Merhaba aşağıdaki komutu çalıştırın ve hello kullanıcı adı ve parola toosign toohello Azure portal kullanın girin.</span><span class="sxs-lookup"><span data-stu-id="75354-118">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="75354-119">Bu hesap için tüm hello abonelikleri komutu tooview aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="75354-119">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="75354-120">Çalışma hello aşağıdaki toowork ile istediğiniz tooselect hello abonelik komutu.</span><span class="sxs-lookup"><span data-stu-id="75354-120">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="75354-121">Değiştir  **&lt;NameOfAzureSubscription** &gt; , Azure aboneliğinizin hello adı.</span><span class="sxs-lookup"><span data-stu-id="75354-121">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="75354-122">Aşağı Not **Subscriptionıd** ve **Tenantıd** bu komutun hello çıktısından.</span><span class="sxs-lookup"><span data-stu-id="75354-122">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="75354-123">Adlı bir Azure kaynak grubu oluşturma **ADFTutorialResourceGroup** hello PowerShell komutunda aşağıdaki hello çalıştırarak.</span><span class="sxs-lookup"><span data-stu-id="75354-123">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="75354-124">Belirttiğiniz Hello kaynak grubu zaten varsa, olup olmadığını tooupdate bunu (Y) veya (N) tutun.</span><span class="sxs-lookup"><span data-stu-id="75354-124">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="75354-125">Farklı bir kaynak grubu kullanıyorsanız, bu öğreticide ADFTutorialResourceGroup yerine, kaynak grubunun toouse hello adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="75354-125">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="75354-126">Bir Azure Active Directory uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75354-126">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="75354-127">Merhaba aşağıdaki hata alırsanız, farklı bir URL belirtin ve hello komutunu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="75354-127">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="75354-128">Merhaba AD hizmet sorumlusu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75354-128">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="75354-129">Hizmet asıl toohello ekleme **veri fabrikası katkıda bulunan** rol.</span><span class="sxs-lookup"><span data-stu-id="75354-129">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="75354-130">Merhaba uygulama kimliği alma</span><span class="sxs-lookup"><span data-stu-id="75354-130">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="75354-131">Merhaba çıktısından hello uygulama kimliği (ApplicationId) aşağı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="75354-131">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="75354-132">Bu adımlardan sonra aşağıdaki dört değere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="75354-132">You should have following four values from these steps:</span></span>

* <span data-ttu-id="75354-133">Kiracı Kimliği</span><span class="sxs-lookup"><span data-stu-id="75354-133">Tenant ID</span></span>
* <span data-ttu-id="75354-134">Abonelik Kimliği</span><span class="sxs-lookup"><span data-stu-id="75354-134">Subscription ID</span></span>
* <span data-ttu-id="75354-135">Uygulama Kimliği</span><span class="sxs-lookup"><span data-stu-id="75354-135">Application ID</span></span>
* <span data-ttu-id="75354-136">Parola (Merhaba ilk komutunda belirtilen)</span><span class="sxs-lookup"><span data-stu-id="75354-136">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="75354-137">Kılavuz</span><span class="sxs-lookup"><span data-stu-id="75354-137">Walkthrough</span></span>
<span data-ttu-id="75354-138">Merhaba kılavuzda data factory kopyalama etkinliği içeren sahip işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75354-138">In hello walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="75354-139">Merhaba kopyalama etkinliği verileri kopyalar aynı blob depolama Merhaba, Azure blob depolama tooanother klasöründe bir klasörden.</span><span class="sxs-lookup"><span data-stu-id="75354-139">hello copy activity copies data from a folder in your Azure blob storage tooanother folder in hello same blob storage.</span></span> 

<span data-ttu-id="75354-140">Merhaba kopya etkinliği Azure Data Factory'de hello veri taşımayı gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="75354-140">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="75354-141">Merhaba etkinlik verileri güvenli, güvenilir ve ölçeklenebilir bir şekilde çeşitli veri depolamaları arasında kopyalayabilirsiniz genel olarak kullanılabilir bir hizmet tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="75354-141">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="75354-142">Bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale hello kopyalama etkinliği hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="75354-142">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

1. <span data-ttu-id="75354-143">Visual Studio 2012/2013/2015'i kullanarak bir C# .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75354-143">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="75354-144">**Visual Studio** 2012/2013/2015’i başlatın.</span><span class="sxs-lookup"><span data-stu-id="75354-144">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="75354-145">Tıklatın **dosya**, çok noktası**yeni**, tıklatıp **proje**.</span><span class="sxs-lookup"><span data-stu-id="75354-145">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="75354-146">**Şablonlar**’ı genişletin ve **Visual C#** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="75354-146">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="75354-147">Bu kılavuzda C# kullanıyor olsanız da dilediğiniz .NET dilini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75354-147">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="75354-148">Seçin **konsol uygulaması** hello sağ proje türlerinde hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="75354-148">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="75354-149">Girin **DataFactoryAPITestApp** hello adı için.</span><span class="sxs-lookup"><span data-stu-id="75354-149">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="75354-150">Seçin **C:\ADFGetStarted** için başlangıç konumu.</span><span class="sxs-lookup"><span data-stu-id="75354-150">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="75354-151">Tıklatın **Tamam** toocreate hello projesi.</span><span class="sxs-lookup"><span data-stu-id="75354-151">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="75354-152">Tıklatın **Araçları**, çok noktası**NuGet Paket Yöneticisi**, tıklatıp **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="75354-152">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="75354-153">Merhaba, **Paket Yöneticisi Konsolu**, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="75354-153">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="75354-154">Komut tooinstall Data Factory paketi aşağıdaki hello çalıştırın:`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="75354-154">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="75354-155">(Active Directory API hello kodda kullandığınız) komutu tooinstall Azure Active Directory paketi aşağıdaki hello çalıştırın:`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="75354-155">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="75354-156">Merhaba Değiştir **App.config** içeriği aşağıdaki hello hello projeyle dosyasında:</span><span class="sxs-lookup"><span data-stu-id="75354-156">Replace hello contents of **App.config** file in hello project with hello following content:</span></span> 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. <span data-ttu-id="75354-157">Merhaba App.Config dosyasında değerlerini güncelleştirin  **&lt;uygulama kimliği&gt;**,  **&lt;parola&gt;**,  **&lt; Abonelik kimliği&gt;**, ve  **&lt;kimliği Kiracı&gt;**  kendi değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="75354-157">In hello App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="75354-158">Merhaba aşağıdakileri ekleyin **kullanarak** deyimleri toohello **Program.cs** hello proje dosyasında.</span><span class="sxs-lookup"><span data-stu-id="75354-158">Add hello following **using** statements toohello **Program.cs** file in hello project.</span></span>

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```
6. <span data-ttu-id="75354-159">Bir örneği oluşturan kodu aşağıdaki hello eklemek **DataPipelineManagementClient** sınıfı toohello **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="75354-159">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="75354-160">Bu nesne toocreate data factory, bağlı hizmet, girdi ve çıktı veri kümelerini ve işlem hattı kullanın.</span><span class="sxs-lookup"><span data-stu-id="75354-160">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="75354-161">Bu nesne toomonitor dilimler bir veri kümesinin ayrıca çalışma zamanında kullanın.</span><span class="sxs-lookup"><span data-stu-id="75354-161">You also use this object toomonitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="75354-162">Merhaba değerini **resourceGroupName** hello Azure kaynak grubu adı.</span><span class="sxs-lookup"><span data-stu-id="75354-162">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span> <span data-ttu-id="75354-163">Hello kullanarak bir kaynak grubu oluşturabilirsiniz [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="75354-163">You can create a resource group using hello [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="75354-164">Merhaba veri fabrikası (dataFactoryName) toobe benzersiz adını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="75354-164">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="75354-165">Merhaba veri fabrikasının adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="75354-165">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="75354-166">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="75354-166">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="75354-167">Oluşturan kod aşağıdaki hello eklemek bir **veri fabrikası** toohello **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="75354-167">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```
8. <span data-ttu-id="75354-168">Oluşturan kod aşağıdaki hello eklemek bir **Azure depolama bağlantılı hizmeti** toohello **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="75354-168">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="75354-169">**storageaccountname** ve **accountkey** sözcüklerini Azure Depolama hesabınızın adı ve anahtarıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="75354-169">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```
9. <span data-ttu-id="75354-170">Oluşturan kod aşağıdaki hello eklemek **giriş ve çıkış veri kümeleri** toohello **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="75354-170">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

    <span data-ttu-id="75354-171">Merhaba **FolderPath** hello giriş blob çok ayarlamak için**adftutorial /** nerede **adftutorial** hello kapsayıcıda blob depolama alanınızın hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="75354-171">hello **FolderPath** for hello input blob is set too**adftutorial/** where **adftutorial** is hello name of hello container in your blob storage.</span></span> <span data-ttu-id="75354-172">Bu kapsayıcı, Azure blob depolamada mevcut değilse, bu ada sahip bir kapsayıcı oluşturmak: **adftutorial** ve bir metin dosyası toohello kapsayıcı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="75354-172">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file toohello container.</span></span>

    <span data-ttu-id="75354-173">Merhaba FolderPath hello için çıktı blob ayarlanır: **adftutorial/apifactoryoutput / {dilim}** nerede **dilim** dinamik olarak hesaplanan göre hello değeri **SliceStart**(tarih-saat her dilimin başlatın.)</span><span class="sxs-lookup"><span data-stu-id="75354-173">hello FolderPath for hello output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on hello value of **SliceStart** (start date-time of each slice.)</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
    
                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
                },
    
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
            }
        }
    });
    ```
10. <span data-ttu-id="75354-174">Merhaba aşağıdaki kod ekleme **oluşturur ve bir ardışık düzen etkinleştirir** toohello **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="75354-174">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="75354-175">Bu işlem hattının **BlobSource**’u bir kaynak olarak, **BlobSink**’i ise bir havuz olarak alan bir **CopyActivity** etkinliği vardır.</span><span class="sxs-lookup"><span data-stu-id="75354-175">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="75354-176">Merhaba kopya etkinliği Azure Data Factory'de hello veri taşımayı gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="75354-176">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="75354-177">Merhaba etkinlik verileri güvenli, güvenilir ve ölçeklenebilir bir şekilde çeşitli veri depolamaları arasında kopyalayabilirsiniz genel olarak kullanılabilir bir hizmet tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="75354-177">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="75354-178">Bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale hello kopyalama etkinliği hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="75354-178">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new PipelineCreateOrUpdateParameters()
    {
        Pipeline = new Pipeline()
        {
            Name = PipelineName,
            Properties = new PipelineProperties()
            {
                Description = "Demo Pipeline for data transfer between blobs",
    
                // Initial value for pipeline's active period. With this, you won't need tooset slice status
                Start = PipelineActivePeriodStartTime,
                End = PipelineActivePeriodEndTime,
    
                Activities = new List<Activity>()
                {
                    new Activity()
                    {
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
                                Name = Dataset_Source
                            }
                        },
                        Outputs = new List<ActivityOutput>()
                        {
                            new ActivityOutput()
                            {
                                Name = Dataset_Destination
                            }
                        },
                        TypeProperties = new CopyActivity()
                        {
                            Source = new BlobSource(),
                            Sink = new BlobSink()
                            {
                                WriteBatchSize = 10000,
                                WriteBatchTimeout = TimeSpan.FromMinutes(10)
                            }
                        }
                    }
    
                },
            }
        }
    });
    ```
12. <span data-ttu-id="75354-179">Aşağıdaki kodu toohello hello eklemek **ana** yöntemi tooget hello hello bir veri dilimin durumunu çıkış veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="75354-179">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="75354-180">Bu örnekte beklenen yalnızca bir dilim yoktur.</span><span class="sxs-lookup"><span data-stu-id="75354-180">There is only one slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");
        // wait before hello next status check
        Thread.Sleep(1000 * 12);
    
        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });
    
        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```
13. <span data-ttu-id="75354-181">**(isteğe bağlı)**  Ekle hello aşağıdaki kod bir veri dilimi toohello çalıştırmak tooget ayrıntılarını **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="75354-181">**(optional)** Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
    Console.ReadKey();
    
    var datasliceRunListResponse = client.DataSliceRuns.List(
        resourceGroupName,
        dataFactoryName,
        Dataset_Destination,
        new DataSliceRunListParameters()
        {
            DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
        });
    
    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }
    
    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```
14. <span data-ttu-id="75354-182">Merhaba tarafından kullanılan yardımcı yöntemini aşağıdaki hello eklemek **ana** yöntemi toohello **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="75354-182">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span> <span data-ttu-id="75354-183">Bu yöntem sağlamanıza olanak tanıyan bir iletişim kutusu açılır **kullanıcı adı** ve **parola** tooAzure Portalı'nda toolog kullanın.</span><span class="sxs-lookup"><span data-stu-id="75354-183">This method pops a dialog box that that lets you provide **user name** and **password** that you use toolog in tooAzure portal.</span></span>

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed tooacquire token");
    }
    ```

15. <span data-ttu-id="75354-184">Merhaba projeyi Hello Çözüm Gezgini, genişletin: **DataFactoryAPITestApp**, sağ **başvuruları**, tıklatıp **Başvuru Ekle**.</span><span class="sxs-lookup"><span data-stu-id="75354-184">In hello Solution Explorer, expand hello project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="75354-185">İçin bu onay kutusunu işaretleyin `System.Configuration` derleme ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="75354-185">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="75354-186">Merhaba konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75354-186">Build hello console application.</span></span> <span data-ttu-id="75354-187">Tıklatın **yapı** hello menüsüne ve ardından üzerinde **yapı çözümü**.</span><span class="sxs-lookup"><span data-stu-id="75354-187">Click **Build** on hello menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="75354-188">Olduğunu en az bir dosya hello adftutorial kapsayıcısında Azure blob depolama alanınızın onaylayın.</span><span class="sxs-lookup"><span data-stu-id="75354-188">Confirm that there is at least one file in hello adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="75354-189">Aksi durumda, Emp.txt dosyasını Not Defteri'nde aşağıdaki hello ile içerik oluşturun ve toohello adftutorial kapsayıcı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="75354-189">If not, create Emp.txt file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="75354-190">Tıklayarak Hello örneği çalıştırmak **hata ayıklama** -> **hata ayıklamayı Başlat** başlangıç menüsünde.</span><span class="sxs-lookup"><span data-stu-id="75354-190">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="75354-191">Merhaba gördüğünüzde **veri dilimi ayrıntılarını çalıştırmak**, birkaç dakika basın için bekleyin ve **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="75354-191">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="75354-192">Kullanım hello Azure portal tooverify bu hello veri fabrikası **APITutorialFactory** yapıları aşağıdaki hello ile oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="75354-192">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
    * <span data-ttu-id="75354-193">Bağlantılı hizmeti: **AzureStorageLinkedService**</span><span class="sxs-lookup"><span data-stu-id="75354-193">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="75354-194">Veri kümesi: **DatasetBlobSource** ve **DatasetBlobDestination**.</span><span class="sxs-lookup"><span data-stu-id="75354-194">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="75354-195">İşlem hattı: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="75354-195">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="75354-196">Bir çıkış dosyası hello oluşturulduğunu doğrulayın **apifactoryoutput** hello klasöründe **adftutorial** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="75354-196">Verify that an output file is created in hello **apifactoryoutput** folder in hello **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="75354-197">Başarısız olan veri dilimlerinin listesini al</span><span class="sxs-lookup"><span data-stu-id="75354-197">Get a list of failed data slices</span></span> 

```csharp
// Parse hello resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a><span data-ttu-id="75354-198">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="75354-198">Next steps</span></span>
<span data-ttu-id="75354-199">Örnek verileri Azure blob depolama tooan Azure SQL veritabanından kopyalar .NET SDK kullanarak bir işlem hattı oluşturmak için aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="75354-199">See hello following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage tooan Azure SQL database:</span></span> 

- [<span data-ttu-id="75354-200">Blob Storage tooSQL veritabanı ' bir ardışık düzen toocopy verileri oluşturma</span><span class="sxs-lookup"><span data-stu-id="75354-200">Create a pipeline toocopy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
