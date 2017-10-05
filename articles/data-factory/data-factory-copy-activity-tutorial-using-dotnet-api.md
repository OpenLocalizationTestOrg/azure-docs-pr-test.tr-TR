---
title: "Öğretici: .NET API kullanarak Kopyalama Etkinlikli bir işlem hattı oluşturma | Microsoft Belgeleri"
description: "Bu öğreticide, .NET API kullanarak Kopyalama Etkinlikli bir Azure Data Factory işlem hattı oluşturursunuz."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 58fc4007-b46d-4c8e-a279-cb9e479b3e2b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 30c7cd1ba455d7b1bc93d76e7ee79455bb52aae9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a><span data-ttu-id="e7430-103">Öğretici: .NET API kullanarak Kopyalama Etkinlikli bir işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e7430-103">Tutorial: Create a pipeline with Copy Activity using .NET API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e7430-104">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e7430-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="e7430-105">Kopyalama Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="e7430-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="e7430-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e7430-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="e7430-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e7430-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="e7430-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7430-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="e7430-109">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="e7430-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="e7430-110">REST API</span><span class="sxs-lookup"><span data-stu-id="e7430-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="e7430-111">.NET API’si</span><span class="sxs-lookup"><span data-stu-id="e7430-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="e7430-112">Bu makalede, Azure blob depolama alanından Azure SQL veritabanına veri kopyalayan bir işlem hattıyla veri fabrikası oluşturmak için [.NET API](https://portal.azure.com)’yi nasıl kullanacağınızı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e7430-112">In this article, you learn how to use [.NET API](https://portal.azure.com) to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="e7430-113">Azure Data Factory’yi ilk kez kullanıyorsanız bu öğreticiyi tamamlamadan önce [Azure Data Factory’ye Giriş](data-factory-introduction.md) makalesini okuyun.</span><span class="sxs-lookup"><span data-stu-id="e7430-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="e7430-114">Bu öğreticide, içinde bir etkinlik olan işlem hattı oluşturursunuz: Kopyalama Etkinliği.</span><span class="sxs-lookup"><span data-stu-id="e7430-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="e7430-115">Kopyalama etkinliği, verileri, desteklenen bir veri deposundan desteklenen bir havuz veri deposuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="e7430-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="e7430-116">Kaynak ve havuz olarak desteklenen veri depolarının listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="e7430-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="e7430-117">Etkinlik, çeşitli veri depolama alanları arasında güvenli, güvenilir ve ölçeklenebilir bir yolla veri kopyalayabilen genel olarak kullanılabilir bir hizmet tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="e7430-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="e7430-118">Kopyalama Etkinliği hakkında daha fazla bilgi için bkz. [Veri Taşıma Etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="e7430-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="e7430-119">Bir işlem hattında birden fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="e7430-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="e7430-120">Bir etkinliğin çıkış veri kümesini diğer etkinliğin giriş veri kümesi olarak ayarlayarak iki etkinliği zincirleyebilir, yani bir etkinliğin diğerinden sonra çalıştırılmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7430-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="e7430-121">Daha fazla bilgi için bkz. [bir işlem hattında birden fazla etkinlik](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="e7430-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="e7430-122">.NET API’deki Data Factory ile ilgili tüm belgeleri görmek için bkz. [Data Factory .NET API Başvurusu](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="e7430-122">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>
> 
> <span data-ttu-id="e7430-123">Bu öğreticideki veri işlem hattı, bir kaynak veri deposundaki verileri hedef veri deposuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="e7430-123">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="e7430-124">Azure Data Factory kullanarak verileri dönüştürme hakkında bir öğretici için bkz. [Öğretici: Hadoop kümesi kullanarak verileri dönüştürmek için işlem hattı oluşturma](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="e7430-124">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7430-125">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e7430-125">Prerequisites</span></span>
* <span data-ttu-id="e7430-126">Öğreticiye genel bir bakış atmak ve **ön koşul** adımlarını tamamlamak için [Öğreticiye Genel Bakış ve Ön Koşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) bölümündeki adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="e7430-126">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to get an overview of the tutorial and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="e7430-127">Visual Studio 2012 veya 2013 veya 2015</span><span class="sxs-lookup"><span data-stu-id="e7430-127">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="e7430-128">[Azure .NET SDK](http://azure.microsoft.com/downloads/)’yı indirip yükleyin</span><span class="sxs-lookup"><span data-stu-id="e7430-128">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span></span>
* <span data-ttu-id="e7430-129">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7430-129">Azure PowerShell.</span></span> <span data-ttu-id="e7430-130">Bilgisayarınıza Azure PowerShell’i yüklemek için [Azure PowerShell’i yükleme ve yapılandırma](../powershell-install-configure.md) makalesindeki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="e7430-130">Follow instructions in [How to install and configure Azure PowerShell](../powershell-install-configure.md) article to install Azure PowerShell on your computer.</span></span> <span data-ttu-id="e7430-131">Azure PowerShell’i kullanarak bir Azure Active Directory uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="e7430-131">You use Azure PowerShell to create an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="e7430-132">Azure Active Directory’de uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="e7430-132">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="e7430-133">Bir Azure Active Directory uygulaması oluşturun, uygulama için bir hizmet sorumlusu oluşturun ve bunu **Data Factory Katılımcısı** rolüne atayın.</span><span class="sxs-lookup"><span data-stu-id="e7430-133">Create an Azure Active Directory application, create a service principal for the application, and assign it to the **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="e7430-134">**PowerShell**’i başlatın.</span><span class="sxs-lookup"><span data-stu-id="e7430-134">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="e7430-135">Aşağıdaki komutu çalıştırın ve Azure portalda oturum açmak için kullandığınız kullanıcı adı ve parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="e7430-135">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="e7430-136">Bu hesapla ilgili tüm abonelikleri görmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e7430-136">Run the following command to view all the subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="e7430-137">Çalışmak isteğiniz aboneliği seçmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e7430-137">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="e7430-138">**&lt;NameOfAzureSubscription**&gt; değerini Azure aboneliğinizin adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e7430-138">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="e7430-139">Bu komutun çıktısından **SubscriptionId** ve **TenantId** değerlerin not alın.</span><span class="sxs-lookup"><span data-stu-id="e7430-139">Note down **SubscriptionId** and **TenantId** from the output of this command.</span></span>

5. <span data-ttu-id="e7430-140">PowerShell’de aşağıdaki komutu çalıştırarak **ADFTutorialResourceGroup** adlı bir Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e7430-140">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="e7430-141">Kaynak grubu zaten varsa bunun güncelleştirileceğini mi (Y) yoksa (N) olarak tutulacağını mı belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7430-141">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="e7430-142">Farklı bir kaynak grubu kullanıyorsanız, bu öğreticide kullanılan ADFTutorialResourceGroup yerine kaynak grubunuzun adını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7430-142">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="e7430-143">Bir Azure Active Directory uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e7430-143">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="e7430-144">Aşağıdaki hatayı alırsanız farklı bir URL belirtip komutu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e7430-144">If you get the following error, specify a different URL and run the command again.</span></span>
    
    ```PowerShell
    Another object with the same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="e7430-145">AD hizmet sorumlusunu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e7430-145">Create the AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="e7430-146">Hizmet sorumlusunu **Data Factory Katılımcısı** rolüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e7430-146">Add service principal to the **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="e7430-147">Uygulama kimliğini alın.</span><span class="sxs-lookup"><span data-stu-id="e7430-147">Get the application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="e7430-148">Çıktıdaki uygulama kimliğini (applicationID) not alın.</span><span class="sxs-lookup"><span data-stu-id="e7430-148">Note down the application ID (applicationID) from the output.</span></span>

<span data-ttu-id="e7430-149">Bu adımlardan sonra aşağıdaki dört değere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e7430-149">You should have following four values from these steps:</span></span>

* <span data-ttu-id="e7430-150">Kiracı Kimliği</span><span class="sxs-lookup"><span data-stu-id="e7430-150">Tenant ID</span></span>
* <span data-ttu-id="e7430-151">Abonelik Kimliği</span><span class="sxs-lookup"><span data-stu-id="e7430-151">Subscription ID</span></span>
* <span data-ttu-id="e7430-152">Uygulama Kimliği</span><span class="sxs-lookup"><span data-stu-id="e7430-152">Application ID</span></span>
* <span data-ttu-id="e7430-153">Parola (ik komutta belirtilir)</span><span class="sxs-lookup"><span data-stu-id="e7430-153">Password (specified in the first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="e7430-154">Kılavuz</span><span class="sxs-lookup"><span data-stu-id="e7430-154">Walkthrough</span></span>
1. <span data-ttu-id="e7430-155">Visual Studio 2012/2013/2015'i kullanarak bir C# .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e7430-155">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="e7430-156">**Visual Studio** 2012/2013/2015’i başlatın.</span><span class="sxs-lookup"><span data-stu-id="e7430-156">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="e7430-157">**Dosya**’ya tıklayın, **Yeni**’nin üzerine gelin ve **Proje**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e7430-157">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="e7430-158">**Şablonlar**’ı genişletin ve **Visual C#** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="e7430-158">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="e7430-159">Bu kılavuzda C# kullanıyor olsanız da dilediğiniz .NET dilini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7430-159">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="e7430-160">Sağ taraftaki proje türleri listesinden **Konsol Uygulaması**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="e7430-160">Select **Console Application** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="e7430-161">Ad için **DataFactoryAPITestApp** değerini girin.</span><span class="sxs-lookup"><span data-stu-id="e7430-161">Enter **DataFactoryAPITestApp** for the Name.</span></span>
   6. <span data-ttu-id="e7430-162">Konum için **C:\ADFGetStarted** yolunu seçin.</span><span class="sxs-lookup"><span data-stu-id="e7430-162">Select **C:\ADFGetStarted** for the Location.</span></span>
   7. <span data-ttu-id="e7430-163">Projeyi oluşturmak için **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e7430-163">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="e7430-164">**Araçlar**'a tıklayın, **NuGet Paket Yöneticisi**'nin üzerine gelin ve ardından **Paket Yöneticisi Konsolu**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e7430-164">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="e7430-165">**Paket Yöneticisi Konsolu**'nda şu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="e7430-165">In the **Package Manager Console**, do the following steps:</span></span>
   1. <span data-ttu-id="e7430-166">Data Factory paketini yüklemek için şu komutu çalıştırın: `Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="e7430-166">Run the following command to install Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="e7430-167">Azure Active Directory paketini yüklemek için şu komutu çalıştırın (kodda Active Directory API'sini kullanırsınız): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="e7430-167">Run the following command to install Azure Active Directory package (you use Active Directory API in the code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="e7430-168">Aşağıdaki **appSetttings** bölümünü **App.config** dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e7430-168">Add the following **appSetttings** section to the **App.config** file.</span></span> <span data-ttu-id="e7430-169">Bu ayarlar **GetAuthorizationHeader** yardımcı yöntemi tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e7430-169">These settings are used by the helper method: **GetAuthorizationHeader**.</span></span>

    <span data-ttu-id="e7430-170">**&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;** ve **&lt;tenant ID&gt;** değerlerini kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e7430-170">Replace values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>

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

5. <span data-ttu-id="e7430-171">Aşağıdaki **using** bildirimlerini projedeki kaynak dosyasına (Program.cs) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e7430-171">Add the following **using** statements to the source file (Program.cs) in the project.</span></span>

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

6. <span data-ttu-id="e7430-172">**DataPipelineManagementClient** sınıfının bir örneğini oluşturan aşağıdaki kodu **Main** yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e7430-172">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span></span> <span data-ttu-id="e7430-173">Bir veri fabrikası, bağlı hizmet, girdi ve çıktı veri kümeleri ve işlem hattı oluşturmak için bu nesneyi kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="e7430-173">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="e7430-174">Çalışma zamanında bir veri kümesinin dilimlerini izlemek için de bu nesneyi kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="e7430-174">You also use this object to monitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client
    string resourceGroupName = "ADFTutorialResourceGroup";
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="e7430-175">**resourceGroupName** değerini Azure kaynak grubunuzun adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e7430-175">Replace the value of **resourceGroupName** with the name of your Azure resource group.</span></span>
   >
   > <span data-ttu-id="e7430-176">Veri fabrikasının adını (dataFactoryName) benzersiz olacak şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="e7430-176">Update name of the data factory (dataFactoryName) to be unique.</span></span> <span data-ttu-id="e7430-177">Veri fabrikasının adı genel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e7430-177">Name of the data factory must be globally unique.</span></span> <span data-ttu-id="e7430-178">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="e7430-178">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>

7. <span data-ttu-id="e7430-179">Bir **veri fabrikası** oluşturan aşağıdaki kodu **Main** yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e7430-179">Add the following code that creates a **data factory** to the **Main** method.</span></span>

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

    <span data-ttu-id="e7430-180">Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e7430-180">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="e7430-181">İşlem hattında bir veya daha fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="e7430-181">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="e7430-182">Örneğin, verileri bir kaynaktan bir hedef veri deposuna kopyalamak için Kopyalama Etkinliği, giriş verilerini ürün çıkış verilerine dönüştürecek Hive betiğini çalıştırmak için de HDInsight Hive etkinliği.</span><span class="sxs-lookup"><span data-stu-id="e7430-182">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="e7430-183">Bu adımda data factory oluşturmayla başlayalım.</span><span class="sxs-lookup"><span data-stu-id="e7430-183">Let's start with creating the data factory in this step.</span></span>
8. <span data-ttu-id="e7430-184">Bir **Azure Depolama bağlı hizmeti** oluşturan aşağıdaki kodu **Main** yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e7430-184">Add the following code that creates an **Azure Storage linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="e7430-185">**storageaccountname** ve **accountkey** sözcüklerini Azure Depolama hesabınızın adı ve anahtarıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e7430-185">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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

    <span data-ttu-id="e7430-186">Veri depolarınızı ve işlem hizmetlerinizi veri fabrikasına bağlamak için veri fabrikasında bağlı hizmetler oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="e7430-186">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="e7430-187">Bu öğreticide, Azure HDInsight veya Azure Data Lake Analytics gibi herhangi bir işlem hizmeti kullanmazsınız.</span><span class="sxs-lookup"><span data-stu-id="e7430-187">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="e7430-188">Azure Depolama (kaynak) ve Azure SQL Veritabanı (hedef) türünde iki veri deposu kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="e7430-188">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

    <span data-ttu-id="e7430-189">Bu nedenle, AzureStorage ve AzureSqlDatabase türlerinde AzureStorageLinkedService ve AzureSqlLinkedService adlı iki bağlı hizmet oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="e7430-189">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

    <span data-ttu-id="e7430-190">AzureStorageLinkedService, Azure depolama hesabınızı veri fabrikasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="e7430-190">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="e7430-191">Bu depolama hesabı, içinde kapsayıcıyı oluşturduğunuz ve verileri [önkoşulların](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) parçası olarak yüklediğiniz hesaptır.</span><span class="sxs-lookup"><span data-stu-id="e7430-191">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
9. <span data-ttu-id="e7430-192">Bir **Azure SQL bağlı hizmeti** oluşturan aşağıdaki kodu **Main** yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e7430-192">Add the following code that creates an **Azure SQL linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="e7430-193">**servername**, **databasename**, **username** ve **password** sözcüklerini Azure SQL sunucunuzun, veritabanınızın, kullanıcınızın adlarıyla ve parolasıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e7430-193">Replace **servername**, **databasename**, **username**, and **password** with names of your Azure SQL server, database, user, and password.</span></span>

    ```csharp
    // create a linked service for output data store: Azure SQL Database
    Console.WriteLine("Creating Azure SQL Database linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureSqlLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureSqlDatabaseLinkedService("Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30")
                )
            }
        }
    );
    ```

    <span data-ttu-id="e7430-194">AzureSqlLinkedService, Azure SQL veritabanınızı veri fabrikasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="e7430-194">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="e7430-195">Blob depolama alanından kopyalanan veriler bu veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="e7430-195">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="e7430-196">Bu veritabanındaki emp tablosunu, [önkoşulların](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) parçası olarak oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="e7430-196">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
10. <span data-ttu-id="e7430-197">**Girdi ve çıktı veri kümeleri** oluşturan aşağıdaki kodu **Main** yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e7430-197">Add the following code that creates **input and output datasets** to the **Main** method.</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "InputDataset";
    string Dataset_Destination = "OutputDataset";

    Console.WriteLine("Creating input dataset of type: Azure Blob");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                Structure = new List<DataElement>()
                {
                    new DataElement() { Name = "FirstName", Type = "String" },
                    new DataElement() { Name = "LastName", Type = "String" }
                },
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

    Console.WriteLine("Creating output dataset of type: Azure SQL");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new DatasetCreateOrUpdateParameters()
        {
            Dataset = new Dataset()
            {
                Name = Dataset_Destination,
                Properties = new DatasetProperties()
                {
                    Structure = new List<DataElement>()
                    {
                        new DataElement() { Name = "FirstName", Type = "String" },
                        new DataElement() { Name = "LastName", Type = "String" }
                    },
                    LinkedServiceName = "AzureSqlLinkedService",
                    TypeProperties = new AzureSqlTableDataset()
                    {
                        TableName = "emp"
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
    
    <span data-ttu-id="e7430-198">Önceki adımda, Azure Depolama hesabınızı ve Azure SQL veritabanınızı veri fabrikanıza bağlamak için bağlı hizmetler oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="e7430-198">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="e7430-199">Bu adımda, sırasıyla AzureStorageLinkedService ve AzureSqlLinkedService tarafından başvurulan veri depolarında depolanan girdi ve çıktı verilerini temsil eden InputDataset ve OutputDataset adlı iki veri kümesini tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="e7430-199">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

    <span data-ttu-id="e7430-200">Azure depolama bağlı hizmeti, Data Factory hizmetinin Azure depolama hesabınıza bağlanmak için çalışma zamanında kullandığı bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="e7430-200">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="e7430-201">Giriş blobu veri kümesi (InputDataset) ise kapsayıcıyı ve girdi verilerini içeren klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="e7430-201">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="e7430-202">Benzer şekilde, Azure SQL Veritabanı bağlı hizmeti, Data Factory hizmetinin Azure SQL veritabanınıza bağlanmak için çalışma zamanında kullandığı bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="e7430-202">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="e7430-203">Çıktı SQL tablosu veri kümesi (OututDataset) ise blob depolama alanındaki verilerin kopyalandığı veritabanında tabloyu belirtir.</span><span class="sxs-lookup"><span data-stu-id="e7430-203">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span>

    <span data-ttu-id="e7430-204">Bu adımda, InputDataset adlı bir veri kümesi oluşturursunuz. Bu veri kümesi, AzureStorageLinkedService bağlı hizmetiyle temsil edilen Azure Depolama’daki bir blob kapsayıcısının (adftutorial) kök klasöründe bulunan blob dosyasını (emp.txt) işaret eder.</span><span class="sxs-lookup"><span data-stu-id="e7430-204">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="e7430-205">fileName için bir değer belirtmezseniz (veya bu adımı atlarsanız) girdi klasöründe bulunan tüm blob’lardaki veriler hedefe kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="e7430-205">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="e7430-206">Bu öğreticide, dosya adı için bir değer belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7430-206">In this tutorial, you specify a value for the fileName.</span></span>    

    <span data-ttu-id="e7430-207">Bu adımda **OutputDataset** adlı bir çıktı veri kümesi oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="e7430-207">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="e7430-208">Bu veri kümesi, **AzureSqlLinkedService** ile temsil edilen Azure SQL veritabanında bir SQL tablosunu işaret eder.</span><span class="sxs-lookup"><span data-stu-id="e7430-208">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService**.</span></span>
11. <span data-ttu-id="e7430-209">**Bir işlem hattı oluşturan ve işlem hattını etkinleştiren** aşağıdaki kodu **Main** yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e7430-209">Add the following code that **creates and activates a pipeline** to the **Main** method.</span></span> <span data-ttu-id="e7430-210">Bu adımda, girdi olarak **InputDataset** ve çıktı olarak **OutputDataset** kullanan **kopyalama etkinliğine** sahip bir işlem hattı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="e7430-210">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2017, 5, 11, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = new DateTime(2017, 5, 12, 0, 0, 0, 0, DateTimeKind.Utc);
    string PipelineName = "ADFTutorialPipeline";

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
                            Name = "BlobToAzureSql",
                            Inputs = new List<ActivityInput>()
                            {
                                new ActivityInput() {
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
                    }
                }
            }
        });
    ```

    <span data-ttu-id="e7430-211">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="e7430-211">Note the following points:</span></span>
   
    - <span data-ttu-id="e7430-212">Etkinlikler bölümünde, **türü** **Copy** olarak ayarlanmış yalnızca bir etkinlik vardır.</span><span class="sxs-lookup"><span data-stu-id="e7430-212">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="e7430-213">Kopyalama etkinliği hakkında daha fazla bilgi için bkz. [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="e7430-213">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="e7430-214">Data Factory çözümlerinde, [veri dönüştürme etkinliklerini](data-factory-data-transformation-activities.md) de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7430-214">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="e7430-215">Etkinlik girdisi **InputDataset** olarak, etkinlik çıktısı ise **OutputDataset** olarak ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e7430-215">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="e7430-216">**typeProperties** bölümünde **BlobSource** kaynak türü, **SqlSink** de havuz türü olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="e7430-216">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="e7430-217">Kaynak ve havuz olarak kopyalama etkinliği tarafından desteklenen veri depolarının eksiksiz listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="e7430-217">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="e7430-218">Kaynak/havuz olarak desteklenen belirli bir veri deposunu nasıl kullanacağınızı öğrenmek için tablodaki bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e7430-218">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
   
    <span data-ttu-id="e7430-219">Şu anda zamanlamayı çıktı veri kümesi yürütmektedir.</span><span class="sxs-lookup"><span data-stu-id="e7430-219">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="e7430-220">Bu öğreticide, çıktı veri kümesi saatte bir dilim oluşturacak şekilde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="e7430-220">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="e7430-221">İşlem hattının başlangıç zamanı ve bitiş zamanı arasında bir gün, yani 24 saat vardır.</span><span class="sxs-lookup"><span data-stu-id="e7430-221">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="e7430-222">Bu nedenle, işlem hattı çıktı veri kümesinden 24 dilim oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e7430-222">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span>
12. <span data-ttu-id="e7430-223">Çıktı veri kümesinin veri diliminin durumunu almak için aşağıdaki kodu **Main** yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e7430-223">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span></span> <span data-ttu-id="e7430-224">Bu örnekte beklenen yalnızca bir dilim vardır.</span><span class="sxs-lookup"><span data-stu-id="e7430-224">There is only slice expected in this sample.</span></span>

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

13. <span data-ttu-id="e7430-225">Bir veri diliminin çalıştırma ayrıntılarını almak için aşağıdaki kodu **Main** yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e7430-225">Add the following code to get run details for a data slice to the **Main** method.</span></span>

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
            }
        );

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

14. <span data-ttu-id="e7430-226">**Main** yöntemi tarafından kullanılan aşağıdaki yardımcı yöntemini **Program** sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e7430-226">Add the following helper method used by the **Main** method to the **Program** class.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e7430-227">Aşağıdaki kodu kopyalayıp yapıştırırken kopyalanan kodun Main yöntemiyle aynı düzeyde olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e7430-227">When you copy and paste the following code, make sure that the copied code is at the same level as the Main method.</span></span>

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

15. <span data-ttu-id="e7430-228">Çözüm Gezgini’nde projeyi (DataFactoryAPITestApp) genişletin, **Başvurular**’a sağ tıklayın ve **Başvuru Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e7430-228">In the Solution Explorer, expand the project (DataFactoryAPITestApp), right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="e7430-229">**System.Configuration** derlemesinin onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="e7430-229">Select check box for **System.Configuration** assembly.</span></span> <span data-ttu-id="e7430-230">**Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e7430-230">and click **OK**.</span></span>
16. <span data-ttu-id="e7430-231">Konsol uygulamasını derleyin.</span><span class="sxs-lookup"><span data-stu-id="e7430-231">Build the console application.</span></span> <span data-ttu-id="e7430-232">Menüde **Derle**’ye tıklayın ve **Çözümü Derle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e7430-232">Click **Build** on the menu and click **Build Solution**.</span></span>
17. <span data-ttu-id="e7430-233">Azure blob depolamanızdaki **adftutorial** kapsayıcısında en az bir dosya olduğunu onaylayın.</span><span class="sxs-lookup"><span data-stu-id="e7430-233">Confirm that there is at least one file in the **adftutorial** container in your Azure blob storage.</span></span> <span data-ttu-id="e7430-234">Aksi takdirde, Not Defteri’nde aşağıdaki içeriklerle **Emp.txt** dosyası oluşturun ve dosyayı adftutorial kapsayıcısına yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e7430-234">If not, create **Emp.txt** file in Notepad with the following content and upload it to the adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
18. <span data-ttu-id="e7430-235">Menüden **Hata Ayıkla** -> **Hata Ayıklamayı Başlat**’a tıklayarak örneği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e7430-235">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span></span> <span data-ttu-id="e7430-236">**Getting run details of a data slice** iletisini gördüğünüzde birkaç dakika bekleyin ve **ENTER** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="e7430-236">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
19. <span data-ttu-id="e7430-237">Azure portalı kullanarak **APITutorialFactory** veri fabrikasının aşağıdaki yapıtlarla birlikte oluşturulduğunu doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="e7430-237">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span></span>
   * <span data-ttu-id="e7430-238">Bağlı hizmet: **LinkedService_AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="e7430-238">Linked service: **LinkedService_AzureStorage**</span></span>
   * <span data-ttu-id="e7430-239">Veri kümesi: **InputDataset** ve **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="e7430-239">Dataset: **InputDataset** and **OutputDataset**.</span></span>
   * <span data-ttu-id="e7430-240">İşlem hattı: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="e7430-240">Pipeline: **PipelineBlobSample**</span></span>
20. <span data-ttu-id="e7430-241">Belirtilen Azure SQL veritabanındaki **emp** tablosunda, iki çalışan kaydının oluşturulduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e7430-241">Verify that the two employee records are created in the **emp** table in the specified Azure SQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7430-242">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e7430-242">Next steps</span></span>
<span data-ttu-id="e7430-243">.NET API’deki Data Factory ile ilgili tüm belgeleri görmek için bkz. [Data Factory .NET API Başvurusu](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="e7430-243">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>

<span data-ttu-id="e7430-244">Bu öğreticide, bir kopyalama işleminde kaynak veri deposu olarak Azure blob depolama alanını ve hedef veri deposu olarak Azure SQL veritabanını kullandınız.</span><span class="sxs-lookup"><span data-stu-id="e7430-244">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="e7430-245">Aşağıdaki tabloda, kopyalama etkinliği tarafından kaynak ve hedef olarak desteklenen veri depolarının listesi sağlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="e7430-245">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="e7430-246">Veri deposundan/veri deposuna veri kopyalama hakkında bilgi edinmek için tablodaki veri deposunun bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e7430-246">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>

