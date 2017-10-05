---
title: "Azure .NET SDK kullanarak veri ardışık düzen oluşturun | Microsoft Docs"
description: "Program aracılığıyla oluşturmak, izlemek ve Data Factory SDK'yı kullanarak Azure data factory'leri yönetme hakkında bilgi edinin."
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
ms.openlocfilehash: 9d9dac75321c5d4e079f49320d9b7c6f56e48754
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="7f1e7-103">Oluşturma, izlemek ve Azure Data Factory .NET SDK kullanarak Azure data factory'leri yönetme</span><span class="sxs-lookup"><span data-stu-id="7f1e7-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="7f1e7-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="7f1e7-104">Overview</span></span>
<span data-ttu-id="7f1e7-105">Oluşturun, izlemek ve program aracılığıyla Data Factory .NET SDK kullanarak Azure data factory'leri yönetin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="7f1e7-106">Bu makalede, oluşturur ve bir veri fabrikası izler örnek bir .NET konsol uygulaması oluşturmak için izleyebileceğiniz bir kılavuz içerir.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-106">This article contains a walkthrough that you can follow to create a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="7f1e7-107">Bu makale, Data Factory .NET API’nin tamamını kapsamaz.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-107">This article does not cover all the Data Factory .NET API.</span></span> <span data-ttu-id="7f1e7-108">Bkz: [Data Factory .NET API Başvurusu](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) hakkında kapsamlı bilgi için .NET API veri fabrikası için.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-108">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7f1e7-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7f1e7-109">Prerequisites</span></span>
* <span data-ttu-id="7f1e7-110">Visual Studio 2012 veya 2013 veya 2015</span><span class="sxs-lookup"><span data-stu-id="7f1e7-110">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="7f1e7-111">İndirme ve yükleme [Azure .NET SDK'sı](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="7f1e7-111">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="7f1e7-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-112">Azure PowerShell.</span></span> <span data-ttu-id="7f1e7-113">Bilgisayarınıza Azure PowerShell’i yüklemek için [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azure/overview) makalesindeki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-113">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install Azure PowerShell on your computer.</span></span> <span data-ttu-id="7f1e7-114">Azure PowerShell’i kullanarak bir Azure Active Directory uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-114">You use Azure PowerShell to create an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="7f1e7-115">Azure Active Directory’de uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f1e7-115">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="7f1e7-116">Bir Azure Active Directory uygulaması oluşturun, uygulama için bir hizmet sorumlusu oluşturun ve bunu **Data Factory Katılımcısı** rolüne atayın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-116">Create an Azure Active Directory application, create a service principal for the application, and assign it to the **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="7f1e7-117">**PowerShell**’i başlatın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-117">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="7f1e7-118">Aşağıdaki komutu çalıştırın ve Azure portalda oturum açmak için kullandığınız kullanıcı adı ve parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-118">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="7f1e7-119">Bu hesapla ilgili tüm abonelikleri görmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-119">Run the following command to view all the subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="7f1e7-120">Çalışmak isteğiniz aboneliği seçmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-120">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="7f1e7-121">**&lt;NameOfAzureSubscription**&gt; değerini Azure aboneliğinizin adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-121">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="7f1e7-122">Bu komutun çıktısından **SubscriptionId** ve **TenantId** değerlerin not alın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-122">Note down **SubscriptionId** and **TenantId** from the output of this command.</span></span>

5. <span data-ttu-id="7f1e7-123">PowerShell’de aşağıdaki komutu çalıştırarak **ADFTutorialResourceGroup** adlı bir Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-123">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="7f1e7-124">Kaynak grubu zaten varsa bunun güncelleştirileceğini mi (Y) yoksa (N) olarak tutulacağını mı belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-124">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="7f1e7-125">Farklı bir kaynak grubu kullanıyorsanız, bu öğreticide kullanılan ADFTutorialResourceGroup yerine kaynak grubunuzun adını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-125">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="7f1e7-126">Bir Azure Active Directory uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-126">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="7f1e7-127">Aşağıdaki hatayı alırsanız farklı bir URL belirtip komutu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-127">If you get the following error, specify a different URL and run the command again.</span></span>
    
    ```PowerShell
    Another object with the same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="7f1e7-128">AD hizmet sorumlusunu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-128">Create the AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="7f1e7-129">Hizmet sorumlusunu **Data Factory Katılımcısı** rolüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-129">Add service principal to the **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="7f1e7-130">Uygulama kimliğini alın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-130">Get the application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="7f1e7-131">Çıktıdaki uygulama kimliğini (applicationID) not alın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-131">Note down the application ID (applicationID) from the output.</span></span>

<span data-ttu-id="7f1e7-132">Bu adımlardan sonra aşağıdaki dört değere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7f1e7-132">You should have following four values from these steps:</span></span>

* <span data-ttu-id="7f1e7-133">Kiracı Kimliği</span><span class="sxs-lookup"><span data-stu-id="7f1e7-133">Tenant ID</span></span>
* <span data-ttu-id="7f1e7-134">Abonelik Kimliği</span><span class="sxs-lookup"><span data-stu-id="7f1e7-134">Subscription ID</span></span>
* <span data-ttu-id="7f1e7-135">Uygulama Kimliği</span><span class="sxs-lookup"><span data-stu-id="7f1e7-135">Application ID</span></span>
* <span data-ttu-id="7f1e7-136">Parola (ik komutta belirtilir)</span><span class="sxs-lookup"><span data-stu-id="7f1e7-136">Password (specified in the first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="7f1e7-137">Kılavuz</span><span class="sxs-lookup"><span data-stu-id="7f1e7-137">Walkthrough</span></span>
<span data-ttu-id="7f1e7-138">Kılavuzda data factory kopyalama etkinliği içeren sahip işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-138">In the walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="7f1e7-139">Kopyalama etkinliği verileri Azure blob depolama alanınızın bir klasörde aynı blob depolama başka bir klasöre kopyalar.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-139">The copy activity copies data from a folder in your Azure blob storage to another folder in the same blob storage.</span></span> 

<span data-ttu-id="7f1e7-140">Kopyalama Etkinliği, Azure Data Factory’de veri hareketini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-140">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="7f1e7-141">Etkinlik, çeşitli veri depolama alanları arasında güvenli, güvenilir ve ölçeklenebilir bir yolla veri kopyalayabilen genel olarak kullanılabilir bir hizmet tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-141">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="7f1e7-142">Kopyalama etkinliği hakkında ayrıntılı bilgi için [Veri Taşıma Etkinlikleri](data-factory-data-movement-activities.md) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-142">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>

1. <span data-ttu-id="7f1e7-143">Visual Studio 2012/2013/2015'i kullanarak bir C# .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-143">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="7f1e7-144">**Visual Studio** 2012/2013/2015’i başlatın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-144">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="7f1e7-145">**Dosya**’ya tıklayın, **Yeni**’nin üzerine gelin ve **Proje**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-145">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="7f1e7-146">**Şablonlar**’ı genişletin ve **Visual C#** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-146">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="7f1e7-147">Bu kılavuzda C# kullanıyor olsanız da dilediğiniz .NET dilini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-147">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="7f1e7-148">Sağ taraftaki proje türleri listesinden **Konsol Uygulaması**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-148">Select **Console Application** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="7f1e7-149">Ad için **DataFactoryAPITestApp** değerini girin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-149">Enter **DataFactoryAPITestApp** for the Name.</span></span>
   6. <span data-ttu-id="7f1e7-150">Konum için **C:\ADFGetStarted** yolunu seçin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-150">Select **C:\ADFGetStarted** for the Location.</span></span>
   7. <span data-ttu-id="7f1e7-151">Projeyi oluşturmak için **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-151">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="7f1e7-152">**Araçlar**'a tıklayın, **NuGet Paket Yöneticisi**'nin üzerine gelin ve ardından **Paket Yöneticisi Konsolu**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-152">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="7f1e7-153">**Paket Yöneticisi Konsolu**'nda şu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="7f1e7-153">In the **Package Manager Console**, do the following steps:</span></span>
   1. <span data-ttu-id="7f1e7-154">Data Factory paketini yüklemek için şu komutu çalıştırın: `Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="7f1e7-154">Run the following command to install Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="7f1e7-155">Azure Active Directory paketini yüklemek için şu komutu çalıştırın (kodda Active Directory API'sini kullanırsınız): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="7f1e7-155">Run the following command to install Azure Active Directory package (you use Active Directory API in the code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="7f1e7-156">Değiştir **App.config** aşağıdaki içeriğe sahip proje dosyasında:</span><span class="sxs-lookup"><span data-stu-id="7f1e7-156">Replace the contents of **App.config** file in the project with the following content:</span></span> 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating the AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. <span data-ttu-id="7f1e7-157">App.Config dosyasında değerlerini güncelleştirin  **&lt;uygulama kimliği&gt;**,  **&lt;parola&gt;**,  **&lt;abonelik kimliği&gt;**, ve  **&lt;kimliği Kiracı&gt;**  kendi değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-157">In the App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="7f1e7-158">Aşağıdakileri ekleyin **kullanarak** deyimlerini **Program.cs** proje dosyasında.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-158">Add the following **using** statements to the **Program.cs** file in the project.</span></span>

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
6. <span data-ttu-id="7f1e7-159">**DataPipelineManagementClient** sınıfının bir örneğini oluşturan aşağıdaki kodu **Main** yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-159">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span></span> <span data-ttu-id="7f1e7-160">Bir veri fabrikası, bağlı hizmet, girdi ve çıktı veri kümeleri ve işlem hattı oluşturmak için bu nesneyi kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-160">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="7f1e7-161">Çalışma zamanında bir veri kümesinin dilimlerini izlemek için de bu nesneyi kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-161">You also use this object to monitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client

    //IMPORTANT: specify the name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: the name of the data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="7f1e7-162">**resourceGroupName** değerini Azure kaynak grubunuzun adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-162">Replace the value of **resourceGroupName** with the name of your Azure resource group.</span></span> <span data-ttu-id="7f1e7-163">Kullanarak bir kaynak grubu oluşturabilirsiniz [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-163">You can create a resource group using the [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="7f1e7-164">Veri fabrikasının adını (dataFactoryName) benzersiz olacak şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-164">Update name of the data factory (dataFactoryName) to be unique.</span></span> <span data-ttu-id="7f1e7-165">Veri fabrikasının adı genel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-165">Name of the data factory must be globally unique.</span></span> <span data-ttu-id="7f1e7-166">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-166">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="7f1e7-167">Bir **veri fabrikası** oluşturan aşağıdaki kodu **Main** yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-167">Add the following code that creates a **data factory** to the **Main** method.</span></span>

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
8. <span data-ttu-id="7f1e7-168">Bir **Azure Depolama bağlı hizmeti** oluşturan aşağıdaki kodu **Main** yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-168">Add the following code that creates an **Azure Storage linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="7f1e7-169">**storageaccountname** ve **accountkey** sözcüklerini Azure Depolama hesabınızın adı ve anahtarıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-169">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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
9. <span data-ttu-id="7f1e7-170">**Girdi ve çıktı veri kümeleri** oluşturan aşağıdaki kodu **Main** yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-170">Add the following code that creates **input and output datasets** to the **Main** method.</span></span>

    <span data-ttu-id="7f1e7-171">**FolderPath** giriş blob ayarlanmıştır **adftutorial /** nerede **adftutorial** blob depolama alanınızın kapsayıcısında adıdır.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-171">The **FolderPath** for the input blob is set to **adftutorial/** where **adftutorial** is the name of the container in your blob storage.</span></span> <span data-ttu-id="7f1e7-172">Bu kapsayıcı, Azure blob depolamada mevcut değilse, bu ada sahip bir kapsayıcı oluşturmak: **adftutorial** ve kapsayıcıya bir metin dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-172">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file to the container.</span></span>

    <span data-ttu-id="7f1e7-173">Çıktı blob FolderPath ayarlamak: **adftutorial/apifactoryoutput / {dilim}** nerede **dilim** dinamik olarak değeri temel alınarak hesaplanır **SliceStart** (tarih-saat her dilimin başlatın.)</span><span class="sxs-lookup"><span data-stu-id="7f1e7-173">The FolderPath for the output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on the value of **SliceStart** (start date-time of each slice.)</span></span>

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
10. <span data-ttu-id="7f1e7-174">**Bir işlem hattı oluşturan ve işlem hattını etkinleştiren** aşağıdaki kodu **Main** yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-174">Add the following code that **creates and activates a pipeline** to the **Main** method.</span></span> <span data-ttu-id="7f1e7-175">Bu işlem hattının **BlobSource**’u bir kaynak olarak, **BlobSink**’i ise bir havuz olarak alan bir **CopyActivity** etkinliği vardır.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-175">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="7f1e7-176">Kopyalama Etkinliği, Azure Data Factory’de veri hareketini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-176">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="7f1e7-177">Etkinlik, çeşitli veri depolama alanları arasında güvenli, güvenilir ve ölçeklenebilir bir yolla veri kopyalayabilen genel olarak kullanılabilir bir hizmet tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-177">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="7f1e7-178">Kopyalama etkinliği hakkında ayrıntılı bilgi için [Veri Taşıma Etkinlikleri](data-factory-data-movement-activities.md) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-178">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>

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
    
                // Initial value for pipeline's active period. With this, you won't need to set slice status
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
12. <span data-ttu-id="7f1e7-179">Çıktı veri kümesinin veri diliminin durumunu almak için aşağıdaki kodu **Main** yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-179">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span></span> <span data-ttu-id="7f1e7-180">Bu örnekte beklenen yalnızca bir dilim yoktur.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-180">There is only one slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling the slice status");
        // wait before the next status check
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
13. <span data-ttu-id="7f1e7-181">**(isteğe bağlı)**  Bir veri dilimi ayrıntılarını çalıştırmak için aşağıdaki kodu ekleyin **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-181">**(optional)** Add the following code to get run details for a data slice to the **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for the output slice to be ready
    Console.WriteLine("\nGive it a few minutes for the output slice to be ready and press any key.");
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
    
    Console.WriteLine("\nPress any key to exit.");
    Console.ReadKey();
    ```
14. <span data-ttu-id="7f1e7-182">**Main** yöntemi tarafından kullanılan aşağıdaki yardımcı yöntemini **Program** sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-182">Add the following helper method used by the **Main** method to the **Program** class.</span></span> <span data-ttu-id="7f1e7-183">Bu yöntem sağlamanıza olanak tanıyan bir iletişim kutusu açılır **kullanıcı adı** ve **parola** , Azure portalında oturum açmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-183">This method pops a dialog box that that lets you provide **user name** and **password** that you use to log in to Azure portal.</span></span>

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

        throw new InvalidOperationException("Failed to acquire token");
    }
    ```

15. <span data-ttu-id="7f1e7-184">Çözüm Gezgini'nde projenizi genişletin: **DataFactoryAPITestApp**, sağ **başvuruları**, tıklatıp **Başvuru Ekle**.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-184">In the Solution Explorer, expand the project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="7f1e7-185">İçin bu onay kutusunu işaretleyin `System.Configuration` derleme ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-185">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="7f1e7-186">Konsol uygulamasını derleyin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-186">Build the console application.</span></span> <span data-ttu-id="7f1e7-187">Menüde **Derle**’ye tıklayın ve **Çözümü Derle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-187">Click **Build** on the menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="7f1e7-188">Olduğunu en az bir dosya adftutorial kapsayıcısında Azure blob depolama alanınızın onaylayın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-188">Confirm that there is at least one file in the adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="7f1e7-189">Aksi durumda, Emp.txt dosyasını Not Defteri'nde aşağıdaki içerik ile oluşturun ve adftutorial kapsayıcıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-189">If not, create Emp.txt file in Notepad with the following content and upload it to the adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="7f1e7-190">Menüden **Hata Ayıkla** -> **Hata Ayıklamayı Başlat**’a tıklayarak örneği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-190">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span></span> <span data-ttu-id="7f1e7-191">**Getting run details of a data slice** iletisini gördüğünüzde birkaç dakika bekleyin ve **ENTER** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-191">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="7f1e7-192">Azure portalı kullanarak **APITutorialFactory** veri fabrikasının aşağıdaki yapıtlarla birlikte oluşturulduğunu doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="7f1e7-192">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span></span>
    * <span data-ttu-id="7f1e7-193">Bağlantılı hizmeti: **AzureStorageLinkedService**</span><span class="sxs-lookup"><span data-stu-id="7f1e7-193">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="7f1e7-194">Veri kümesi: **DatasetBlobSource** ve **DatasetBlobDestination**.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-194">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="7f1e7-195">İşlem hattı: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="7f1e7-195">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="7f1e7-196">Bir çıkış dosyası oluşturulur doğrulayın **apifactoryoutput** klasöründe **adftutorial** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="7f1e7-196">Verify that an output file is created in the **apifactoryoutput** folder in the **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="7f1e7-197">Başarısız olan veri dilimlerinin listesini al</span><span class="sxs-lookup"><span data-stu-id="7f1e7-197">Get a list of failed data slices</span></span> 

```csharp
// Parse the resource path
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

## <a name="next-steps"></a><span data-ttu-id="7f1e7-198">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7f1e7-198">Next steps</span></span>
<span data-ttu-id="7f1e7-199">Verileri Azure blob depolama alanından Azure SQL veritabanına kopyalar .NET SDK kullanarak bir işlem hattı oluşturmak için aşağıdaki örneğe bakın:</span><span class="sxs-lookup"><span data-stu-id="7f1e7-199">See the following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage to an Azure SQL database:</span></span> 

- [<span data-ttu-id="7f1e7-200">Blob depolama alanından SQL veritabanına veri kopyalamak için bir işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f1e7-200">Create a pipeline to copy data from Blob Storage to SQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
