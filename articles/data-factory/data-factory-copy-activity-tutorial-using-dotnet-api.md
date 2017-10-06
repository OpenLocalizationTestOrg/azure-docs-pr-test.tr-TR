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
ms.openlocfilehash: 52f72da54cdd80691e09d7453bf6730454c4089e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a><span data-ttu-id="1ac6e-103">Öğretici: .NET API kullanarak Kopyalama Etkinlikli bir işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ac6e-103">Tutorial: Create a pipeline with Copy Activity using .NET API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1ac6e-104">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1ac6e-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="1ac6e-105">Kopyalama Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="1ac6e-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="1ac6e-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1ac6e-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="1ac6e-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ac6e-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="1ac6e-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ac6e-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="1ac6e-109">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="1ac6e-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="1ac6e-110">REST API</span><span class="sxs-lookup"><span data-stu-id="1ac6e-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="1ac6e-111">.NET API’si</span><span class="sxs-lookup"><span data-stu-id="1ac6e-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="1ac6e-112">Bu makalede, bilgi nasıl toouse [.NET API](https://portal.azure.com) toocreate data factory Azure blob depolama tooan Azure SQL veritabanına verileri kopyalayan bir işlem hattı ile.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-112">In this article, you learn how toouse [.NET API](https://portal.azure.com) toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="1ac6e-113">Yeni tooAzure Data Factory varsa, hello okuma [giriş tooAzure Data Factory](data-factory-introduction.md) Bu öğretici yapmadan önce makalesi.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="1ac6e-114">Bu öğreticide, içinde bir etkinlik olan işlem hattı oluşturursunuz: Kopyalama Etkinliği.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="1ac6e-115">Merhaba kopyalama etkinliği bir desteklenen veri deposu tooa desteklenen havuz veri deposundan verileri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="1ac6e-116">Kaynak ve havuz olarak desteklenen veri depolarının listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="1ac6e-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="1ac6e-117">Merhaba etkinlik verileri güvenli, güvenilir ve ölçeklenebilir bir şekilde çeşitli veri depolamaları arasında kopyalayabilirsiniz genel olarak kullanılabilir bir hizmet tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="1ac6e-118">Merhaba kopyalama etkinliği hakkında daha fazla bilgi için bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="1ac6e-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="1ac6e-119">Bir işlem hattında birden fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="1ac6e-120">Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="1ac6e-121">Daha fazla bilgi için bkz. [bir işlem hattında birden fazla etkinlik](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="1ac6e-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="1ac6e-122">.NET API’deki Data Factory ile ilgili tüm belgeleri görmek için bkz. [Data Factory .NET API Başvurusu](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="1ac6e-122">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>
> 
> <span data-ttu-id="1ac6e-123">Merhaba veri ardışık Bu öğreticide, bir kaynak veri deposu tooa hedef veri deposundan verileri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-123">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="1ac6e-124">Nasıl bir öğretici için Azure Data Factory kullanarak tootransform verileri görmek [Öğreticisi: Hadoop kümesi kullanarak bir ardışık düzen tootransform veri derleme](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="1ac6e-124">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ac6e-125">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1ac6e-125">Prerequisites</span></span>
* <span data-ttu-id="1ac6e-126">Git üzerinden [öğreticiye genel bakış ve ön koşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget hello öğretici ve tam hello genel bakış **önkoşul** adımları.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-126">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget an overview of hello tutorial and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="1ac6e-127">Visual Studio 2012 veya 2013 veya 2015</span><span class="sxs-lookup"><span data-stu-id="1ac6e-127">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="1ac6e-128">[Azure .NET SDK](http://azure.microsoft.com/downloads/)’yı indirip yükleyin</span><span class="sxs-lookup"><span data-stu-id="1ac6e-128">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span></span>
* <span data-ttu-id="1ac6e-129">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-129">Azure PowerShell.</span></span> <span data-ttu-id="1ac6e-130">' Ndaki yönergeleri izleyin [nasıl tooinstall Azure PowerShell'i ve yapılandırma](../powershell-install-configure.md) tooinstall Azure PowerShell, bilgisayarınızda makalesi.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-130">Follow instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="1ac6e-131">Azure PowerShell toocreate bir Azure Active Directory uygulamasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-131">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="1ac6e-132">Azure Active Directory’de uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ac6e-132">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="1ac6e-133">Bir Azure Active Directory uygulaması oluşturmak, Merhaba uygulaması için bir hizmet sorumlusu oluşturmak ve toohello atamak **veri fabrikası katkıda bulunan** rol.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-133">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="1ac6e-134">**PowerShell**’i başlatın.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-134">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="1ac6e-135">Merhaba aşağıdaki komutu çalıştırın ve hello kullanıcı adı ve parola toosign toohello Azure portal kullanın girin.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="1ac6e-136">Bu hesap için tüm hello abonelikleri komutu tooview aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-136">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="1ac6e-137">Çalışma hello aşağıdaki toowork ile istediğiniz tooselect hello abonelik komutu.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="1ac6e-138">Değiştir  **&lt;NameOfAzureSubscription** &gt; , Azure aboneliğinizin hello adı.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-138">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="1ac6e-139">Aşağı Not **Subscriptionıd** ve **Tenantıd** bu komutun hello çıktısından.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-139">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="1ac6e-140">Adlı bir Azure kaynak grubu oluşturma **ADFTutorialResourceGroup** hello PowerShell komutunda aşağıdaki hello çalıştırarak.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-140">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="1ac6e-141">Belirttiğiniz Hello kaynak grubu zaten varsa, olup olmadığını tooupdate bunu (Y) veya (N) tutun.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-141">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="1ac6e-142">Farklı bir kaynak grubu kullanıyorsanız, bu öğreticide ADFTutorialResourceGroup yerine, kaynak grubunun toouse hello adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-142">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="1ac6e-143">Bir Azure Active Directory uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-143">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="1ac6e-144">Merhaba aşağıdaki hata alırsanız, farklı bir URL belirtin ve hello komutunu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-144">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="1ac6e-145">Merhaba AD hizmet sorumlusu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-145">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="1ac6e-146">Hizmet asıl toohello ekleme **veri fabrikası katkıda bulunan** rol.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-146">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="1ac6e-147">Merhaba uygulama kimliği alma</span><span class="sxs-lookup"><span data-stu-id="1ac6e-147">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="1ac6e-148">Merhaba çıktısından hello uygulama kimliği (ApplicationId) aşağı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-148">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="1ac6e-149">Bu adımlardan sonra aşağıdaki dört değere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1ac6e-149">You should have following four values from these steps:</span></span>

* <span data-ttu-id="1ac6e-150">Kiracı Kimliği</span><span class="sxs-lookup"><span data-stu-id="1ac6e-150">Tenant ID</span></span>
* <span data-ttu-id="1ac6e-151">Abonelik Kimliği</span><span class="sxs-lookup"><span data-stu-id="1ac6e-151">Subscription ID</span></span>
* <span data-ttu-id="1ac6e-152">Uygulama Kimliği</span><span class="sxs-lookup"><span data-stu-id="1ac6e-152">Application ID</span></span>
* <span data-ttu-id="1ac6e-153">Parola (Merhaba ilk komutunda belirtilen)</span><span class="sxs-lookup"><span data-stu-id="1ac6e-153">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="1ac6e-154">Kılavuz</span><span class="sxs-lookup"><span data-stu-id="1ac6e-154">Walkthrough</span></span>
1. <span data-ttu-id="1ac6e-155">Visual Studio 2012/2013/2015'i kullanarak bir C# .NET konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-155">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="1ac6e-156">**Visual Studio** 2012/2013/2015’i başlatın.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-156">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="1ac6e-157">Tıklatın **dosya**, çok noktası**yeni**, tıklatıp **proje**.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-157">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="1ac6e-158">**Şablonlar**’ı genişletin ve **Visual C#** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-158">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="1ac6e-159">Bu kılavuzda C# kullanıyor olsanız da dilediğiniz .NET dilini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-159">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="1ac6e-160">Seçin **konsol uygulaması** hello sağ proje türlerinde hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-160">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="1ac6e-161">Girin **DataFactoryAPITestApp** hello adı için.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-161">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="1ac6e-162">Seçin **C:\ADFGetStarted** için başlangıç konumu.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-162">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="1ac6e-163">Tıklatın **Tamam** toocreate hello projesi.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-163">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="1ac6e-164">Tıklatın **Araçları**, çok noktası**NuGet Paket Yöneticisi**, tıklatıp **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-164">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="1ac6e-165">Merhaba, **Paket Yöneticisi Konsolu**, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="1ac6e-165">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="1ac6e-166">Komut tooinstall Data Factory paketi aşağıdaki hello çalıştırın:`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="1ac6e-166">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="1ac6e-167">(Active Directory API hello kodda kullandığınız) komutu tooinstall Azure Active Directory paketi aşağıdaki hello çalıştırın:`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="1ac6e-167">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="1ac6e-168">Merhaba aşağıdakileri ekleyin **appSetttings** bölüm toohello **App.config** dosya.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-168">Add hello following **appSetttings** section toohello **App.config** file.</span></span> <span data-ttu-id="1ac6e-169">Bu ayarlar hello yardımcı yöntemi tarafından kullanılır: **GetAuthorizationHeader**.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-169">These settings are used by hello helper method: **GetAuthorizationHeader**.</span></span>

    <span data-ttu-id="1ac6e-170">**&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;** ve **&lt;tenant ID&gt;** değerlerini kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-170">Replace values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>

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

5. <span data-ttu-id="1ac6e-171">Merhaba aşağıdakileri ekleyin **kullanarak** hello projesindeki deyimleri toohello kaynak dosyasını (Program.cs).</span><span class="sxs-lookup"><span data-stu-id="1ac6e-171">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

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

6. <span data-ttu-id="1ac6e-172">Bir örneği oluşturan kodu aşağıdaki hello eklemek **DataPipelineManagementClient** sınıfı toohello **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-172">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="1ac6e-173">Bu nesne toocreate data factory, bağlı hizmet, girdi ve çıktı veri kümelerini ve işlem hattı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-173">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="1ac6e-174">Bu nesne toomonitor dilimler bir veri kümesinin ayrıca çalışma zamanında kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-174">You also use this object toomonitor slices of a dataset at runtime.</span></span>

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
   > <span data-ttu-id="1ac6e-175">Merhaba değerini **resourceGroupName** hello Azure kaynak grubu adı.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-175">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span>
   >
   > <span data-ttu-id="1ac6e-176">Merhaba veri fabrikası (dataFactoryName) toobe benzersiz adını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-176">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="1ac6e-177">Merhaba veri fabrikasının adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-177">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="1ac6e-178">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-178">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>

7. <span data-ttu-id="1ac6e-179">Oluşturan kod aşağıdaki hello eklemek bir **veri fabrikası** toohello **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-179">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

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

    <span data-ttu-id="1ac6e-180">Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-180">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="1ac6e-181">İşlem hattında bir veya daha fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-181">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="1ac6e-182">Örneğin, bir kopyalama etkinliği toocopy verilerinden bir kaynak tooa hedef veri deposu ve Hdınsight Hive etkinliği toorun bir Hive betiği tootransform veri tooproduct çıktı verileri girin.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-182">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="1ac6e-183">Bu adımda hello data factory oluşturmayla başlayalım.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-183">Let's start with creating hello data factory in this step.</span></span>
8. <span data-ttu-id="1ac6e-184">Oluşturan kod aşağıdaki hello eklemek bir **Azure depolama bağlantılı hizmeti** toohello **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-184">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="1ac6e-185">**storageaccountname** ve **accountkey** sözcüklerini Azure Depolama hesabınızın adı ve anahtarıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-185">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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

    <span data-ttu-id="1ac6e-186">Verilerinizi depolayan ve Hizmetleri toohello veri fabrikası işlem bir veri fabrikası toolink bağlı hizmetler oluşturma.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-186">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="1ac6e-187">Bu öğreticide, Azure HDInsight veya Azure Data Lake Analytics gibi herhangi bir işlem hizmeti kullanmazsınız.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-187">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="1ac6e-188">Azure Depolama (kaynak) ve Azure SQL Veritabanı (hedef) türünde iki veri deposu kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-188">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

    <span data-ttu-id="1ac6e-189">Bu nedenle, AzureStorage ve AzureSqlDatabase türlerinde AzureStorageLinkedService ve AzureSqlLinkedService adlı iki bağlı hizmet oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-189">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

    <span data-ttu-id="1ac6e-190">Merhaba AzureStorageLinkedService Azure depolama hesabı toohello veri fabrikanıza bağlar.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-190">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="1ac6e-191">Bu depolama hesap hello biri, hangi, kapsayıcı oluşturuldu ve hello veri parçası olarak yüklenen [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="1ac6e-191">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
9. <span data-ttu-id="1ac6e-192">Oluşturan kod aşağıdaki hello eklemek bir **Azure SQL bağlı hizmeti** toohello **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-192">Add hello following code that creates an **Azure SQL linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="1ac6e-193">**servername**, **databasename**, **username** ve **password** sözcüklerini Azure SQL sunucunuzun, veritabanınızın, kullanıcınızın adlarıyla ve parolasıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-193">Replace **servername**, **databasename**, **username**, and **password** with names of your Azure SQL server, database, user, and password.</span></span>

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

    <span data-ttu-id="1ac6e-194">AzureSqlLinkedService Azure SQL veritabanı toohello veri fabrikanıza bağlar.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-194">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="1ac6e-195">Merhaba blob depolama biriminden kopyalanan hello veriler bu veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-195">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="1ac6e-196">Bu veritabanında hello emp tablosunda bir parçası olarak oluşturulan [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="1ac6e-196">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
10. <span data-ttu-id="1ac6e-197">Oluşturan kod aşağıdaki hello eklemek **giriş ve çıkış veri kümeleri** toohello **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-197">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

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
    
    <span data-ttu-id="1ac6e-198">Merhaba önceki adımda, Azure Storage hesabını ve Azure SQL veritabanı tooyour veri fabrikası bağlı hizmetler toolink oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-198">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="1ac6e-199">Bu adımda, iki veri kümesi InputDataset ve giriş temsil OutputDataset ve sırasıyla AzureStorageLinkedService ve Azuresqllinkedservice'in başvurduğu hello veri depolarında depolanan çıktı verilerini adlı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-199">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

    <span data-ttu-id="1ac6e-200">Hello Azure depolama bağlı hizmeti çalışma zamanı tooconnect tooyour Azure depolama hesabı Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-200">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="1ac6e-201">Ve hello giriş blob veri kümesi (InputDataset) hello kapsayıcı ve hello giriş verisi içeren hello klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-201">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="1ac6e-202">Benzer şekilde, hello Azure SQL veritabanı bağlantılı hizmet çalışma zamanı tooconnect tooyour Azure SQL veritabanını Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-202">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="1ac6e-203">Ve kopyalanan verileri hello blob depolama biriminden hello veritabanı toowhich hello SQL tablosu veri kümesi (OututDataset) hello tabloda hello çıktı.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-203">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

    <span data-ttu-id="1ac6e-204">Bu adımda, tooa blob dosya (emp.txt) işaret InputDataset adlı bir veri hello kök klasöründe bir blob kapsayıcısını (adftutorial) hello Azure hello AzureStorageLinkedService bağlı hizmeti tarafından temsil edilen depolama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-204">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="1ac6e-205">Verme hello dosya adı için bir değer belirtin (veya atlayın) hello giriş klasöründeki tüm blob'lara ait veriler kopyalanan toohello hedef demektir.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-205">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="1ac6e-206">Bu öğreticide, hello dosya adı için bir değer belirtin.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-206">In this tutorial, you specify a value for hello fileName.</span></span>    

    <span data-ttu-id="1ac6e-207">Bu adımda **OutputDataset** adlı bir çıktı veri kümesi oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-207">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="1ac6e-208">Bu veri kümesi tarafından temsil edilen hello Azure SQL veritabanındaki tooa SQL tablosunu işaret **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-208">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span>
11. <span data-ttu-id="1ac6e-209">Merhaba aşağıdaki kod ekleme **oluşturur ve bir ardışık düzen etkinleştirir** toohello **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-209">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="1ac6e-210">Bu adımda, girdi olarak **InputDataset** ve çıktı olarak **OutputDataset** kullanan **kopyalama etkinliğine** sahip bir işlem hattı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-210">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

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

                    // Initial value for pipeline's active period. With this, you won't need tooset slice status
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

    <span data-ttu-id="1ac6e-211">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="1ac6e-211">Note hello following points:</span></span>
   
    - <span data-ttu-id="1ac6e-212">Merhaba etkinlikler bölümünde, yalnızca bir etkinlik olduğundan, **türü** çok ayarlanır**kopya**.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-212">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="1ac6e-213">Merhaba kopyalama etkinliği hakkında daha fazla bilgi için bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="1ac6e-213">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="1ac6e-214">Data Factory çözümlerinde, [veri dönüştürme etkinliklerini](data-factory-data-transformation-activities.md) de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-214">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="1ac6e-215">Merhaba etkinlik çok kümesi için giriş**InputDataset** ve hello etkinlik çok kümesi için çıkış**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-215">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="1ac6e-216">Merhaba, **typeProperties** bölümünde **BlobSource** hello kaynak türü olarak belirtilir ve **SqlSink** hello Havuz türü olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-216">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="1ac6e-217">Kaynakları ve havuzlarını olarak hello kopyalama etkinliği tarafından desteklenen veri depoları tam bir listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="1ac6e-217">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="1ac6e-218">nasıl toouse belirli bir desteklenen veri depolayan bir kaynak/havuz toolearn hello tablosundaki hello bağlantısını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-218">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
   
    <span data-ttu-id="1ac6e-219">Şu anda, hangi sürücü zamanlama hello çıktı veri kümesi değil.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-219">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="1ac6e-220">Bu öğreticide, çıktı veri kümesi yapılandırılmış tooproduce bir dilim saate birdir.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-220">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="1ac6e-221">bir başlangıç saati ve bir 24 saat olan günü birbirinden, bitiş zamanı Hello ardışık düzen vardır.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-221">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="1ac6e-222">Bu nedenle, çıktı veri kümesinin 24 dilim hello ardışık düzen tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-222">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span>
12. <span data-ttu-id="1ac6e-223">Aşağıdaki kodu toohello hello eklemek **ana** yöntemi tooget hello hello bir veri dilimin durumunu çıkış veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-223">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="1ac6e-224">Bu örnekte beklenen yalnızca bir dilim vardır.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-224">There is only slice expected in this sample.</span></span>

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

13. <span data-ttu-id="1ac6e-225">Aşağıdaki kodu çalıştırmak tooget ayrıntılara veri dilimi toohello için hello eklemek **ana** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-225">Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

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

    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```

14. <span data-ttu-id="1ac6e-226">Merhaba tarafından kullanılan yardımcı yöntemini aşağıdaki hello eklemek **ana** yöntemi toohello **Program** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-226">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1ac6e-227">Hello aşağıdaki kodu kopyalayıp, o hello emin olun kopyalanan kodu aynı düzeydeki hello ana yöntem hello adresindeki.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-227">When you copy and paste hello following code, make sure that hello copied code is at hello same level as hello Main method.</span></span>

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

15. <span data-ttu-id="1ac6e-228">Buna Çözüm Gezgini Merhaba, Merhaba projeyi (DataFactoryAPITestApp) genişletin, sağ **başvuruları**, tıklatıp **Başvuru Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-228">In hello Solution Explorer, expand hello project (DataFactoryAPITestApp), right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="1ac6e-229">**System.Configuration** derlemesinin onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-229">Select check box for **System.Configuration** assembly.</span></span> <span data-ttu-id="1ac6e-230">**Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-230">and click **OK**.</span></span>
16. <span data-ttu-id="1ac6e-231">Merhaba konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-231">Build hello console application.</span></span> <span data-ttu-id="1ac6e-232">Tıklatın **yapı** hello menüsüne ve ardından üzerinde **yapı çözümü**.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-232">Click **Build** on hello menu and click **Build Solution**.</span></span>
17. <span data-ttu-id="1ac6e-233">Hello en az bir dosya olduğundan emin olun **adftutorial** , Azure blob depolamada kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-233">Confirm that there is at least one file in hello **adftutorial** container in your Azure blob storage.</span></span> <span data-ttu-id="1ac6e-234">Değilse, oluşturmak **Emp.txt** Not Defteri'nde içeriği aşağıdaki hello ile dosya ve toohello adftutorial kapsayıcı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-234">If not, create **Emp.txt** file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
18. <span data-ttu-id="1ac6e-235">Tıklayarak Hello örneği çalıştırmak **hata ayıklama** -> **hata ayıklamayı Başlat** başlangıç menüsünde.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-235">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="1ac6e-236">Merhaba gördüğünüzde **veri dilimi ayrıntılarını çalıştırmak**, birkaç dakika basın için bekleyin ve **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-236">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
19. <span data-ttu-id="1ac6e-237">Kullanım hello Azure portal tooverify bu hello veri fabrikası **APITutorialFactory** yapıları aşağıdaki hello ile oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="1ac6e-237">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
   * <span data-ttu-id="1ac6e-238">Bağlı hizmet: **LinkedService_AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="1ac6e-238">Linked service: **LinkedService_AzureStorage**</span></span>
   * <span data-ttu-id="1ac6e-239">Veri kümesi: **InputDataset** ve **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-239">Dataset: **InputDataset** and **OutputDataset**.</span></span>
   * <span data-ttu-id="1ac6e-240">İşlem hattı: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="1ac6e-240">Pipeline: **PipelineBlobSample**</span></span>
20. <span data-ttu-id="1ac6e-241">Merhaba iki çalışan kayıtları hello oluşturulduğunu doğrulayın **emp** hello tablosunda belirtilen Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-241">Verify that hello two employee records are created in hello **emp** table in hello specified Azure SQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ac6e-242">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1ac6e-242">Next steps</span></span>
<span data-ttu-id="1ac6e-243">.NET API’deki Data Factory ile ilgili tüm belgeleri görmek için bkz. [Data Factory .NET API Başvurusu](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="1ac6e-243">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>

<span data-ttu-id="1ac6e-244">Bu öğreticide, bir kopyalama işleminde kaynak veri deposu olarak Azure blob depolama alanını ve hedef veri deposu olarak Azure SQL veritabanını kullandınız.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-244">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="1ac6e-245">Merhaba aşağıdaki tabloda kaynakları ve hedefleri hello kopyalama etkinliği tarafından desteklenen veri depoları listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1ac6e-245">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="1ac6e-246">nasıl bir veri öğesine/öğesinden toocopy veri deposu hakkında toolearn hello veri deposu hello tablosundaki hello bağlantısını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1ac6e-246">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>

