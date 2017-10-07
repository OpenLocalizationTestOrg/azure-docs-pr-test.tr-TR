---
title: "Öğretici: Kullanım REST API'si toocreate bir Azure Data Factory işlem hattı | Microsoft Docs"
description: "Bu öğreticide, Azure blob depolamadan Azure SQL veritabanını kopyalama etkinliği toocopy verilerle REST API toocreate bir Azure Data Factory işlem hattı kullanın."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1704cdf8-30ad-49bc-a71c-4057e26e7350
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: aa6c9b035101c4ff9acff90117ca6e3e7067f418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="8be63-103">Öğretici: Kullanım REST API'si toocreate bir Azure Data Factory işlem hattı toocopy veri</span><span class="sxs-lookup"><span data-stu-id="8be63-103">Tutorial: Use REST API toocreate an Azure Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8be63-104">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="8be63-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="8be63-105">Kopyalama Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="8be63-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="8be63-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8be63-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="8be63-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8be63-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="8be63-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8be63-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="8be63-109">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="8be63-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="8be63-110">REST API</span><span class="sxs-lookup"><span data-stu-id="8be63-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="8be63-111">.NET API’si</span><span class="sxs-lookup"><span data-stu-id="8be63-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="8be63-112">Bu makalede, nasıl toouse REST API toocreate data factory Azure blob depolama tooan Azure SQL veritabanına verileri kopyalayan bir işlem hattı ile bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="8be63-112">In this article, you learn how toouse REST API toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="8be63-113">Yeni tooAzure Data Factory varsa, hello okuma [giriş tooAzure Data Factory](data-factory-introduction.md) Bu öğretici yapmadan önce makalesi.</span><span class="sxs-lookup"><span data-stu-id="8be63-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="8be63-114">Bu öğreticide, içinde bir etkinlik olan işlem hattı oluşturursunuz: Kopyalama Etkinliği.</span><span class="sxs-lookup"><span data-stu-id="8be63-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="8be63-115">Merhaba kopyalama etkinliği bir desteklenen veri deposu tooa desteklenen havuz veri deposundan verileri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="8be63-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="8be63-116">Kaynak ve havuz olarak desteklenen veri depolarının listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="8be63-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="8be63-117">Merhaba etkinlik verileri güvenli, güvenilir ve ölçeklenebilir bir şekilde çeşitli veri depolamaları arasında kopyalayabilirsiniz genel olarak kullanılabilir bir hizmet tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="8be63-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="8be63-118">Merhaba kopyalama etkinliği hakkında daha fazla bilgi için bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="8be63-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="8be63-119">Bir işlem hattında birden fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="8be63-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="8be63-120">Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir.</span><span class="sxs-lookup"><span data-stu-id="8be63-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="8be63-121">Daha fazla bilgi için bkz. [bir işlem hattında birden fazla etkinlik](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="8be63-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="8be63-122">Bu makalede, tüm hello veri fabrikası REST API kapsamaz.</span><span class="sxs-lookup"><span data-stu-id="8be63-122">This article does not cover all hello Data Factory REST API.</span></span> <span data-ttu-id="8be63-123">Data Factory cmdlet’leri hakkında kapsamlı belgeler için bkz. [Data Factory REST API Başvurusu](/rest/api/datafactory/).</span><span class="sxs-lookup"><span data-stu-id="8be63-123">See [Data Factory REST API Reference](/rest/api/datafactory/) for comprehensive documentation on Data Factory cmdlets.</span></span>
>  
> <span data-ttu-id="8be63-124">Merhaba veri ardışık Bu öğreticide, bir kaynak veri deposu tooa hedef veri deposundan verileri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="8be63-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="8be63-125">Nasıl bir öğretici için Azure Data Factory kullanarak tootransform verileri görmek [Öğreticisi: Hadoop kümesi kullanarak bir ardışık düzen tootransform veri derleme](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="8be63-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8be63-126">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8be63-126">Prerequisites</span></span>
* <span data-ttu-id="8be63-127">Git üzerinden [öğreticiye genel bakış](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) ve tam hello **önkoşul** adımları.</span><span class="sxs-lookup"><span data-stu-id="8be63-127">Go through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="8be63-128">[Curl](https://curl.haxx.se/dlwiz/) aracını makinenize yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8be63-128">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="8be63-129">REST komutları toocreate data factory hello Curl aracını kullanın.</span><span class="sxs-lookup"><span data-stu-id="8be63-129">You use hello Curl tool with REST commands toocreate a data factory.</span></span> 
* <span data-ttu-id="8be63-130">Aşağıdakileri yapmak için [bu makaledeki](../azure-resource-manager/resource-group-create-service-principal-portal.md) yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="8be63-130">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span> 
  1. <span data-ttu-id="8be63-131">Azure Active Directory’de **ADFCopyTutorialApp** adlı bir Web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8be63-131">Create a Web application named **ADFCopyTutorialApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="8be63-132">**İstemci kimliği** ve **gizli anahtarı** alın.</span><span class="sxs-lookup"><span data-stu-id="8be63-132">Get **client ID** and **secret key**.</span></span> 
  3. <span data-ttu-id="8be63-133">**İstemci kimliğini** alın.</span><span class="sxs-lookup"><span data-stu-id="8be63-133">Get **tenant ID**.</span></span> 
  4. <span data-ttu-id="8be63-134">Merhaba atamak **ADFCopyTutorialApp** uygulama toohello **veri fabrikası katkıda bulunan** rol.</span><span class="sxs-lookup"><span data-stu-id="8be63-134">Assign hello **ADFCopyTutorialApp** application toohello **Data Factory Contributor** role.</span></span>  
* <span data-ttu-id="8be63-135">[Azure PowerShell](/powershell/azure/overview)'i yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8be63-135">Install [Azure PowerShell](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="8be63-136">Başlatma **PowerShell** ve adımları izleyerek hello.</span><span class="sxs-lookup"><span data-stu-id="8be63-136">Launch **PowerShell** and do hello following steps.</span></span> <span data-ttu-id="8be63-137">Bu öğreticide hello sonuna kadar Azure PowerShell'i açık tutun.</span><span class="sxs-lookup"><span data-stu-id="8be63-137">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="8be63-138">Kapatıp yeniden açın, toorun hello komutları yeniden gerekir.</span><span class="sxs-lookup"><span data-stu-id="8be63-138">If you close and reopen, you need toorun hello commands again.</span></span>
  
  1. <span data-ttu-id="8be63-139">Merhaba aşağıdaki komutu çalıştırın ve hello kullanıcı adı ve parola toosign toohello Azure portalını kullanın girin:</span><span class="sxs-lookup"><span data-stu-id="8be63-139">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. <span data-ttu-id="8be63-140">Komut tooview aşağıdaki hello hello abonelikler bu hesap için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8be63-140">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. <span data-ttu-id="8be63-141">Çalışma hello aşağıdaki toowork ile istediğiniz tooselect hello abonelik komutu.</span><span class="sxs-lookup"><span data-stu-id="8be63-141">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="8be63-142">Değiştir  **&lt;NameOfAzureSubscription** &gt; , Azure aboneliğinizin hello adı.</span><span class="sxs-lookup"><span data-stu-id="8be63-142">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span> 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. <span data-ttu-id="8be63-143">Adlı bir Azure kaynak grubu oluşturma **ADFTutorialResourceGroup** hello PowerShell komutunda aşağıdaki hello çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="8be63-143">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      <span data-ttu-id="8be63-144">Belirttiğiniz Hello kaynak grubu zaten varsa, olup olmadığını tooupdate bunu (Y) veya (N) tutun.</span><span class="sxs-lookup"><span data-stu-id="8be63-144">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span> 
     
      <span data-ttu-id="8be63-145">Merhaba bu öğreticideki adımlardan bazıları ADFTutorialResourceGroup adlı hello kaynak grubunu kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="8be63-145">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="8be63-146">Farklı bir kaynak grubu kullanıyorsanız, bu öğreticide ADFTutorialResourceGroup yerine, kaynak grubunun toouse hello adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="8be63-146">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="8be63-147">JSON tanımları oluşturma</span><span class="sxs-lookup"><span data-stu-id="8be63-147">Create JSON definitions</span></span>
<span data-ttu-id="8be63-148">JSON dosyaları curl.exe bulunduğu hello klasöründe aşağıdaki oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8be63-148">Create following JSON files in hello folder where curl.exe is located.</span></span> 

### <a name="datafactoryjson"></a><span data-ttu-id="8be63-149">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="8be63-149">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8be63-150">Tooprefix/sonek ADFCopyTutorialDF toomake isteyebilirsiniz adı genel olarak benzersiz olmalıdır, benzersiz bir ad.</span><span class="sxs-lookup"><span data-stu-id="8be63-150">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span> 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="8be63-151">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="8be63-151">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8be63-152">**accountname** ve **accountkey** sözcüklerini Azure depolama hesabınızın adı ve anahtarıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8be63-152">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="8be63-153">toolearn tooget depolama alanınızın nasıl erişim anahtar, bkz: [erişim anahtarlarını görüntüleme, kopyalama ve yeniden oluşturma depolama](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="8be63-153">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

<span data-ttu-id="8be63-154">JSON özellikleri hakkındaki ayrıntılar için bkz. [Azure Depolama bağlı hizmeti](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="8be63-154">For details about JSON properties, see [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span></span>

### <a name="azuersqllinkedservicejson"></a><span data-ttu-id="8be63-155">azuersqllinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="8be63-155">azuersqllinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8be63-156">Değiştir **servername**, **databasename**, **kullanıcıadı**, ve **parola** , SQL veritabanı adını, Azure SQL sunucunuzun adıyla kullanıcı Hesap ve hello hesabının parolası.</span><span class="sxs-lookup"><span data-stu-id="8be63-156">Replace **servername**, **databasename**, **username**, and **password** with name of your Azure SQL server, name of SQL database, user account, and password for hello account.</span></span>  
> 
>

```JSON
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

<span data-ttu-id="8be63-157">JSON özellikleri hakkındaki ayrıntılar için bkz. [Azure SQL bağlı hizmeti](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8be63-157">For details about JSON properties, see [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="8be63-158">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="8be63-158">inputdataset.json</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "structure": [
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "AzureStorageLinkedService",
    "typeProperties": {
      "folderPath": "adftutorial/",
      "fileName": "emp.txt",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ","
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="8be63-159">Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:</span><span class="sxs-lookup"><span data-stu-id="8be63-159">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="8be63-160">Özellik</span><span class="sxs-lookup"><span data-stu-id="8be63-160">Property</span></span> | <span data-ttu-id="8be63-161">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8be63-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="8be63-162">type</span><span class="sxs-lookup"><span data-stu-id="8be63-162">type</span></span> | <span data-ttu-id="8be63-163">Merhaba type özelliği çok ayarlamak**AzureBlob** verileri Azure blob depolama alanında bulunduğundan.</span><span class="sxs-lookup"><span data-stu-id="8be63-163">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
| <span data-ttu-id="8be63-164">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="8be63-164">linkedServiceName</span></span> | <span data-ttu-id="8be63-165">Toohello başvuruyor **AzureStorageLinkedService** daha önce oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="8be63-165">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="8be63-166">folderPath</span><span class="sxs-lookup"><span data-stu-id="8be63-166">folderPath</span></span> | <span data-ttu-id="8be63-167">Merhaba blob belirtir **kapsayıcı** ve hello **klasörü** giriş BLOB'ları içerir.</span><span class="sxs-lookup"><span data-stu-id="8be63-167">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="8be63-168">Bu öğreticide adftutorial hello blob kapsayıcı ve hello kök klasör.</span><span class="sxs-lookup"><span data-stu-id="8be63-168">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
| <span data-ttu-id="8be63-169">fileName</span><span class="sxs-lookup"><span data-stu-id="8be63-169">fileName</span></span> | <span data-ttu-id="8be63-170">Bu özellik isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8be63-170">This property is optional.</span></span> <span data-ttu-id="8be63-171">Bu özelliği atarsanız, tüm dosyaları hello folderPath çekilir.</span><span class="sxs-lookup"><span data-stu-id="8be63-171">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="8be63-172">Bu öğreticide **emp.txt** hello fileName, böylece yalnızca bu dosyanın işleme için kayıt için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="8be63-172">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
| <span data-ttu-id="8be63-173">format -> type</span><span class="sxs-lookup"><span data-stu-id="8be63-173">format -> type</span></span> |<span data-ttu-id="8be63-174">Merhaba giriş dosyası kullanırız hello metin biçiminde olduğundan **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="8be63-174">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
| <span data-ttu-id="8be63-175">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="8be63-175">columnDelimiter</span></span> | <span data-ttu-id="8be63-176">Merhaba giriş dosyası Hello sütunlarında tarafından ayrılmış **virgül karakteriyle (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="8be63-176">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
| <span data-ttu-id="8be63-177">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="8be63-177">frequency/interval</span></span> | <span data-ttu-id="8be63-178">Merhaba sıklığını çok ayarlamak**saat** ve aralığı çok ayarlamak**1**, o hello yani dilimler kullanılabilir giriş **saatlik**.</span><span class="sxs-lookup"><span data-stu-id="8be63-178">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="8be63-179">Hello Data Factory hizmeti için giriş verileri saatte hello kök klasöründe blob kapsayıcısının diğer bir deyişle, görünüyor (**adftutorial**), belirtilen.</span><span class="sxs-lookup"><span data-stu-id="8be63-179">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="8be63-180">Merhaba veri hello ardışık düzen başlangıç ve bitiş zamanları, değil önce veya sonra bu kez içinde arar.</span><span class="sxs-lookup"><span data-stu-id="8be63-180">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
| <span data-ttu-id="8be63-181">external</span><span class="sxs-lookup"><span data-stu-id="8be63-181">external</span></span> | <span data-ttu-id="8be63-182">Bu özellik çok ayarlanır**true** hello verileri bu ardışık düzen tarafından oluşturulmamış olması durumunda.</span><span class="sxs-lookup"><span data-stu-id="8be63-182">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="8be63-183">Bu öğreticide girdi verileri Hello Biz bu özellik tootrue ayarlamak için bu ardışık düzen tarafından oluşturulmayan hello emp.txt, dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="8be63-183">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

<span data-ttu-id="8be63-184">Bu JSON özellikleri hakkında daha fazla bilgi için bkz. [Azure Blob bağlayıcısı makalesi](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8be63-184">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>

### <a name="outputdatasetjson"></a><span data-ttu-id="8be63-185">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="8be63-185">outputdataset.json</span></span>

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "structure": [
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "emp"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="8be63-186">Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:</span><span class="sxs-lookup"><span data-stu-id="8be63-186">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="8be63-187">Özellik</span><span class="sxs-lookup"><span data-stu-id="8be63-187">Property</span></span> | <span data-ttu-id="8be63-188">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8be63-188">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="8be63-189">type</span><span class="sxs-lookup"><span data-stu-id="8be63-189">type</span></span> | <span data-ttu-id="8be63-190">Merhaba type özelliği çok ayarlamak**AzureSqlTable** verileri bir Azure SQL veritabanı tablosunda kopyalanan tooa olduğundan.</span><span class="sxs-lookup"><span data-stu-id="8be63-190">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
| <span data-ttu-id="8be63-191">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="8be63-191">linkedServiceName</span></span> | <span data-ttu-id="8be63-192">Toohello başvuruyor **AzureSqlLinkedService** daha önce oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="8be63-192">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="8be63-193">tableName</span><span class="sxs-lookup"><span data-stu-id="8be63-193">tableName</span></span> | <span data-ttu-id="8be63-194">Belirtilen hello **tablo** toowhich hello veri kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="8be63-194">Specified hello **table** toowhich hello data is copied.</span></span> | 
| <span data-ttu-id="8be63-195">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="8be63-195">frequency/interval</span></span> | <span data-ttu-id="8be63-196">Merhaba sıklığı çok ayarlı**saat** ve aralığı **1**, hello çıkış dilimler üretilir anlamına gelir **saatlik** hello ardışık düzen başlangıç ve bitiş zamanları, önce değil arasında veya Bu kez sonra.</span><span class="sxs-lookup"><span data-stu-id="8be63-196">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

<span data-ttu-id="8be63-197">Üç sütun – **kimliği**, **FirstName**, ve **LastName** – hello veritabanındaki emp tablosunda hello.</span><span class="sxs-lookup"><span data-stu-id="8be63-197">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="8be63-198">Kimliktir bir kimlik sütunu yalnızca toospecify gereken şekilde **FirstName** ve **LastName** burada.</span><span class="sxs-lookup"><span data-stu-id="8be63-198">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

<span data-ttu-id="8be63-199">Bu JSON özellikleri hakkında daha fazla bilgi için bkz. [Azure SQL bağlayıcısı makalesi](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8be63-199">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="8be63-200">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="8be63-200">pipeline.json</span></span>

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data tooAzure SQL database",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2017-05-11T00:00:00Z",
    "end": "2017-05-12T00:00:00Z"
  }
}
```

<span data-ttu-id="8be63-201">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="8be63-201">Note hello following points:</span></span>

- <span data-ttu-id="8be63-202">Merhaba etkinlikler bölümünde, yalnızca bir etkinlik olduğundan, **türü** çok ayarlanır**kopya**.</span><span class="sxs-lookup"><span data-stu-id="8be63-202">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="8be63-203">Merhaba kopyalama etkinliği hakkında daha fazla bilgi için bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="8be63-203">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="8be63-204">Data Factory çözümlerinde, [veri dönüştürme etkinliklerini](data-factory-data-transformation-activities.md) de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8be63-204">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
- <span data-ttu-id="8be63-205">Merhaba etkinlik çok kümesi için giriş**Azureblobınput** ve hello etkinlik çok kümesi için çıkış**AzureSqlOutput**.</span><span class="sxs-lookup"><span data-stu-id="8be63-205">Input for hello activity is set too**AzureBlobInput** and output for hello activity is set too**AzureSqlOutput**.</span></span> 
- <span data-ttu-id="8be63-206">Merhaba, **typeProperties** bölümünde **BlobSource** hello kaynak türü olarak belirtilir ve **SqlSink** hello Havuz türü olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="8be63-206">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="8be63-207">Kaynakları ve havuzlarını olarak hello kopyalama etkinliği tarafından desteklenen veri depoları tam bir listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="8be63-207">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="8be63-208">nasıl toouse belirli bir desteklenen veri depolayan bir kaynak/havuz toolearn hello tablosundaki hello bağlantısını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8be63-208">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
 
<span data-ttu-id="8be63-209">Merhaba Hello değerini değiştirin **Başlat** hello geçerli gün özelliğiyle ve **son** hello sonraki gün değeri.</span><span class="sxs-lookup"><span data-stu-id="8be63-209">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="8be63-210">Yalnızca hello tarih bölümünü belirtip tarih saat hello hello saat bölümünü atlayın.</span><span class="sxs-lookup"><span data-stu-id="8be63-210">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="8be63-211">Örneğin, "2017-02-çok eşdeğeri olan 03", "2017-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="8be63-211">For example, "2017-02-03", which is equivalent too"2017-02-03T00:00:00Z"</span></span>
 
<span data-ttu-id="8be63-212">Başlangıç ve bitiş tarih saatleri [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8be63-212">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="8be63-213">Örneğin: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="8be63-213">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="8be63-214">Merhaba **son** saati isteğe bağlıdır ancak biz Bu öğreticide kullanın.</span><span class="sxs-lookup"><span data-stu-id="8be63-214">hello **end** time is optional, but we use it in this tutorial.</span></span> 
 
<span data-ttu-id="8be63-215">Hello için değer belirtmezseniz, **son** özelliği olarak hesaplanır "**start + 48 saat**".</span><span class="sxs-lookup"><span data-stu-id="8be63-215">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="8be63-216">toorun hello ardışık kalıcı olarak belirtmek **9999-09-09** hello hello değeri olarak **son** özelliği.</span><span class="sxs-lookup"><span data-stu-id="8be63-216">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
 
<span data-ttu-id="8be63-217">Örnek önceki hello vardır 24 veri dilimi her veri dilimi saatlik oluşturulduğundan.</span><span class="sxs-lookup"><span data-stu-id="8be63-217">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

<span data-ttu-id="8be63-218">İşlem hattı tanımındaki JSON özelliklerinin açıklamaları için [işlem hatları oluşturma](data-factory-create-pipelines.md) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="8be63-218">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="8be63-219">Kopyalama etkinliği tanımındaki JSON özelliklerinin açıklamaları için bkz. [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="8be63-219">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="8be63-220">BlobSource tarafından desteklenen JSON özelliklerinin açıklamaları için bkz. [Azure Blob bağlayıcısı makalesi](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="8be63-220">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="8be63-221">SqlSink tarafından desteklenen JSON özelliklerinin açıklamaları için bkz. [Azure SQL Veritabanı bağlayıcısı makalesi](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="8be63-221">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="set-global-variables"></a><span data-ttu-id="8be63-222">Genel değişkenleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="8be63-222">Set global variables</span></span>
<span data-ttu-id="8be63-223">Azure PowerShell'de komutları hello değerleri kendi değerlerinizle değiştirerek sonra aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="8be63-223">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8be63-224">İstemci kimliği, istemci parolası, kiracı kimliği ve abonelik kimliğini edinme konusunda yönergeler için [Önkoşullar](#prerequisites) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="8be63-224">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

<span data-ttu-id="8be63-225">Kullanmakta olduğunuz hello veri fabrikasının hello adı güncelleştirdikten sonra komut aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8be63-225">Run hello following command after updating hello name of hello data factory you are using:</span></span> 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a><span data-ttu-id="8be63-226">AAD ile kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="8be63-226">Authenticate with AAD</span></span>
<span data-ttu-id="8be63-227">Komut tooauthenticate ile Azure Active Directory (AAD) aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8be63-227">Run hello following command tooauthenticate with Azure Active Directory (AAD):</span></span> 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a><span data-ttu-id="8be63-228">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="8be63-228">Create data factory</span></span>
<span data-ttu-id="8be63-229">Bu adımda, **ADFCopyTutorialDF** adlı bir Azure Data Factory oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="8be63-229">In this step, you create an Azure Data Factory named **ADFCopyTutorialDF**.</span></span> <span data-ttu-id="8be63-230">Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8be63-230">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="8be63-231">İşlem hattında bir veya daha fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="8be63-231">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="8be63-232">Örneğin, bir kopyalama etkinliği toocopy veri kaynağı tooa hedef veri deposu.</span><span class="sxs-lookup"><span data-stu-id="8be63-232">For example, a Copy Activity toocopy data from a source tooa destination data store.</span></span> <span data-ttu-id="8be63-233">Hdınsight Hive etkinliği toorun bir Hive betiği tootransform veri tooproduct çıktı verileri girin.</span><span class="sxs-lookup"><span data-stu-id="8be63-233">A HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="8be63-234">Aşağıdaki komutları toocreate hello veri fabrikası hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8be63-234">Run hello following commands toocreate hello data factory:</span></span> 

1. <span data-ttu-id="8be63-235">Adlı hello komutu toovariable Ata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="8be63-235">Assign hello command toovariable named **cmd**.</span></span> 
   
    > [!IMPORTANT]
    > <span data-ttu-id="8be63-236">Burada belirttiğiniz (ADFCopyTutorialDF) eşleşmeleri hello hello belirtilen adı hello veri fabrikası bu hello adını onaylayın **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="8be63-236">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. <span data-ttu-id="8be63-237">Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="8be63-237">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="8be63-238">Merhaba sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="8be63-238">View hello results.</span></span> <span data-ttu-id="8be63-239">Merhaba veri fabrikası başarıyla oluşturuldu, hello JSON hello hello veri fabrikasında için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="8be63-239">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>  
   
    ```
    Write-Host $results
    ```

<span data-ttu-id="8be63-240">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="8be63-240">Note hello following points:</span></span>

* <span data-ttu-id="8be63-241">Merhaba hello Azure Data Factory adı küresel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8be63-241">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="8be63-242">Sonuçları hello hata görürseniz: **veri fabrikası adı "ADFCopyTutorialDF" kullanılabilir değil**, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="8be63-242">If you see hello error in results: **Data factory name “ADFCopyTutorialDF” is not available**, do hello following steps:</span></span>  
  
  1. <span data-ttu-id="8be63-243">Merhaba değişiklik hello adı (örneğin, yournameADFCopyTutorialDF) **datafactory.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="8be63-243">Change hello name (for example, yournameADFCopyTutorialDF) in hello **datafactory.json** file.</span></span>
  2. <span data-ttu-id="8be63-244">Merhaba ilk komutta burada hello **$cmd** değişken değeri atanır, ADFCopyTutorialDF hello yeni adıyla değiştirin ve hello komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8be63-244">In hello first command where hello **$cmd** variable is assigned a value, replace ADFCopyTutorialDF with hello new name and run hello command.</span></span> 
  3. <span data-ttu-id="8be63-245">Merhaba sonraki iki komutları tooinvoke hello REST API toocreate hello veri fabrikası ve yazdırma hello sonuçlarını hello işlemi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8be63-245">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span> 
     
     <span data-ttu-id="8be63-246">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="8be63-246">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="8be63-247">toocreate Data Factory örnekleri toobe katılımcı/yönetici rolünüz hello Azure aboneliği gerekir</span><span class="sxs-lookup"><span data-stu-id="8be63-247">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="8be63-248">hello veri fabrikası Hello adı hello gelecekte bir DNS adı olarak kayıtlı ve bu nedenle herkese görünür hale gelir.</span><span class="sxs-lookup"><span data-stu-id="8be63-248">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="8be63-249">Merhaba hatayı alırsanız: "**Bu abonelik, Microsoft.DataFactory kayıtlı toouse ad değil**" Merhaba aşağıdakilerden birini yapın ve yeniden yayımlamayı deneyin:</span><span class="sxs-lookup"><span data-stu-id="8be63-249">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="8be63-250">Azure PowerShell'de komut tooregister hello Data Factory sağlayıcısının aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8be63-250">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="8be63-251">Bu Data Factory sağlayıcısının kayıtlı hello komutu tooconfirm aşağıdaki hello çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8be63-251">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="8be63-252">Oturum açma kullanılarak hello hello Azure aboneliğinize [Azure portal](https://portal.azure.com) ve tooa Data Factory dikey penceresine gidin (veya) hello Azure portalında bir data factory oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8be63-252">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="8be63-253">Bu eylemin hello sağlayıcıyı sizin için otomatik olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="8be63-253">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="8be63-254">Bir işlem hattı oluşturmadan önce toocreate birkaç Data Factory varlıklarını önce gerekir.</span><span class="sxs-lookup"><span data-stu-id="8be63-254">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="8be63-255">İlk bağlı hizmetler toolink kaynağı oluşturun ve hedef veri depolayan tooyour veri depolayın.</span><span class="sxs-lookup"><span data-stu-id="8be63-255">You first create linked services toolink source and destination data stores tooyour data store.</span></span> <span data-ttu-id="8be63-256">Ardından, girdi ve çıktı veri kümeleri toorepresent verileri bağlı veri depolarında tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8be63-256">Then, define input and output datasets toorepresent data in linked data stores.</span></span> <span data-ttu-id="8be63-257">Son olarak, bu veri kümeleri kullanan bir etkinlik hello ardışık düzen oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8be63-257">Finally, create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="8be63-258">Bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="8be63-258">Create linked services</span></span>
<span data-ttu-id="8be63-259">Verilerinizi depolayan ve Hizmetleri toohello veri fabrikası işlem bir veri fabrikası toolink bağlı hizmetler oluşturma.</span><span class="sxs-lookup"><span data-stu-id="8be63-259">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="8be63-260">Bu öğreticide, Azure HDInsight veya Azure Data Lake Analytics gibi herhangi bir işlem hizmeti kullanmazsınız.</span><span class="sxs-lookup"><span data-stu-id="8be63-260">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="8be63-261">Azure Depolama (kaynak) ve Azure SQL Veritabanı (hedef) türünde iki veri deposu kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="8be63-261">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> <span data-ttu-id="8be63-262">Bu nedenle, AzureStorage ve AzureSqlDatabase türlerinde AzureStorageLinkedService ve AzureSqlLinkedService adlı iki bağlı hizmet oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="8be63-262">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="8be63-263">Merhaba AzureStorageLinkedService Azure depolama hesabı toohello veri fabrikanıza bağlar.</span><span class="sxs-lookup"><span data-stu-id="8be63-263">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="8be63-264">Bu depolama hesap hello biri, hangi, kapsayıcı oluşturuldu ve hello veri parçası olarak yüklenen [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="8be63-264">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="8be63-265">AzureSqlLinkedService Azure SQL veritabanı toohello veri fabrikanıza bağlar.</span><span class="sxs-lookup"><span data-stu-id="8be63-265">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="8be63-266">Merhaba blob depolama biriminden kopyalanan hello veriler bu veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="8be63-266">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="8be63-267">Bu veritabanında hello emp tablosunda bir parçası olarak oluşturulan [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="8be63-267">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="8be63-268">Azure Storage bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="8be63-268">Create Azure Storage linked service</span></span>
<span data-ttu-id="8be63-269">Bu adımda, Azure depolama hesabı tooyour veri fabrikanıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="8be63-269">In this step, you link your Azure storage account tooyour data factory.</span></span> <span data-ttu-id="8be63-270">Bu bölümde hello adı ve Azure depolama hesabınızın anahtarı belirtin.</span><span class="sxs-lookup"><span data-stu-id="8be63-270">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="8be63-271">Bkz: [Azure depolama bağlantılı hizmeti](data-factory-azure-blob-connector.md#azure-storage-linked-service) JSON kullanılan özellikler toodefine hakkında ayrıntılı bilgi için bir Azure Storage bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="8be63-271">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>  

1. <span data-ttu-id="8be63-272">Adlı hello komutu toovariable Ata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="8be63-272">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="8be63-273">Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="8be63-273">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="8be63-274">Merhaba sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="8be63-274">View hello results.</span></span> <span data-ttu-id="8be63-275">Merhaba bağlı hizmet başarıyla oluşturuldu, hello JSON hello hello bağlantılı hizmeti için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="8be63-275">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a><span data-ttu-id="8be63-276">Azure SQL bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="8be63-276">Create Azure SQL linked service</span></span>
<span data-ttu-id="8be63-277">Bu adımda, Azure SQL veritabanı tooyour veri fabrikanıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="8be63-277">In this step, you link your Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="8be63-278">Bu bölümde hello Azure SQL sunucu adı, veritabanı adı, kullanıcı adı ve parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="8be63-278">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="8be63-279">Bkz: [Azure SQL bağlı hizmeti](data-factory-azure-sql-connector.md#linked-service-properties) JSON kullanılan özellikler toodefine hakkındaki ayrıntılar için hizmeti bir Azure SQL bağlı.</span><span class="sxs-lookup"><span data-stu-id="8be63-279">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used toodefine an Azure SQL linked service.</span></span>

1. <span data-ttu-id="8be63-280">Adlı hello komutu toovariable Ata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="8be63-280">Assign hello command toovariable named **cmd**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="8be63-281">Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="8be63-281">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="8be63-282">Merhaba sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="8be63-282">View hello results.</span></span> <span data-ttu-id="8be63-283">Merhaba bağlı hizmet başarıyla oluşturuldu, hello JSON hello hello bağlantılı hizmeti için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="8be63-283">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="8be63-284">Veri kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="8be63-284">Create datasets</span></span>
<span data-ttu-id="8be63-285">Merhaba önceki adımda, Azure Storage hesabını ve Azure SQL veritabanı tooyour veri fabrikası bağlı hizmetler toolink oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="8be63-285">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="8be63-286">Bu adımda, iki veri kümesi Azureblobınput ve giriş temsil AzureSqlOutput ve sırasıyla AzureStorageLinkedService ve Azuresqllinkedservice'in başvurduğu hello veri depolarında depolanan çıktı verilerini adlı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="8be63-286">In this step, you define two datasets named AzureBlobInput and AzureSqlOutput that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="8be63-287">Hello Azure depolama bağlı hizmeti çalışma zamanı tooconnect tooyour Azure depolama hesabı Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="8be63-287">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="8be63-288">Ve hello giriş blob veri kümesi (Azureblobınput) hello kapsayıcı ve hello giriş verisi içeren hello klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="8be63-288">And, hello input blob dataset (AzureBlobInput) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="8be63-289">Benzer şekilde, hello Azure SQL veritabanı bağlantılı hizmet çalışma zamanı tooconnect tooyour Azure SQL veritabanını Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="8be63-289">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="8be63-290">Ve kopyalanan verileri hello blob depolama biriminden hello veritabanı toowhich hello SQL tablosu veri kümesi (OututDataset) hello tabloda hello çıktı.</span><span class="sxs-lookup"><span data-stu-id="8be63-290">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="8be63-291">Girdi veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="8be63-291">Create input dataset</span></span>
<span data-ttu-id="8be63-292">Bu adımda, tooa blob dosya (emp.txt) işaret Azureblobınput adlı bir veri hello kök klasöründe bir blob kapsayıcısını (adftutorial) hello Azure hello AzureStorageLinkedService bağlı hizmeti tarafından temsil edilen depolama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8be63-292">In this step, you create a dataset named AzureBlobInput that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="8be63-293">Verme hello dosya adı için bir değer belirtin (veya atlayın) hello giriş klasöründeki tüm blob'lara ait veriler kopyalanan toohello hedef demektir.</span><span class="sxs-lookup"><span data-stu-id="8be63-293">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="8be63-294">Bu öğreticide, hello dosya adı için bir değer belirtin.</span><span class="sxs-lookup"><span data-stu-id="8be63-294">In this tutorial, you specify a value for hello fileName.</span></span> 

1. <span data-ttu-id="8be63-295">Adlı hello komutu toovariable Ata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="8be63-295">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="8be63-296">Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="8be63-296">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="8be63-297">Merhaba sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="8be63-297">View hello results.</span></span> <span data-ttu-id="8be63-298">Merhaba veri kümesi başarıyla oluşturuldu, hello JSON hello hello kümesinde için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="8be63-298">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="8be63-299">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="8be63-299">Create output dataset</span></span>
<span data-ttu-id="8be63-300">Hello Azure SQL veritabanı bağlantılı hizmet çalışma zamanı tooconnect tooyour Azure SQL veritabanını Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="8be63-300">hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="8be63-301">Bu adımda oluşturduğunuz hello çıktı SQL tablosu veri kümesi (OututDataset) hello veritabanı toowhich hello verileri hello blob depolama biriminden hello tabloda kopyalanır belirtir.</span><span class="sxs-lookup"><span data-stu-id="8be63-301">hello output SQL table dataset (OututDataset) you create in this step specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

1. <span data-ttu-id="8be63-302">Adlı hello komutu toovariable Ata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="8be63-302">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="8be63-303">Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="8be63-303">Run hello command by using **Invoke-Command**.</span></span>
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="8be63-304">Merhaba sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="8be63-304">View hello results.</span></span> <span data-ttu-id="8be63-305">Merhaba veri kümesi başarıyla oluşturuldu, hello JSON hello hello kümesinde için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="8be63-305">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a><span data-ttu-id="8be63-306">İşlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8be63-306">Create pipeline</span></span>
<span data-ttu-id="8be63-307">Bu adımda, girdi olarak **AzureBlobInput**, çıktı olaraksa **AzureSqlOutput** kullanan bir **kopyalama etkinliğine** sahip bir işlem hattı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="8be63-307">In this step, you create a pipeline with a **copy activity** that uses **AzureBlobInput** as an input and **AzureSqlOutput** as an output.</span></span>

<span data-ttu-id="8be63-308">Şu anda, hangi sürücü zamanlama hello çıktı veri kümesi değil.</span><span class="sxs-lookup"><span data-stu-id="8be63-308">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="8be63-309">Bu öğreticide, çıktı veri kümesi yapılandırılmış tooproduce bir dilim saate birdir.</span><span class="sxs-lookup"><span data-stu-id="8be63-309">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="8be63-310">bir başlangıç saati ve bir 24 saat olan günü birbirinden, bitiş zamanı Hello ardışık düzen vardır.</span><span class="sxs-lookup"><span data-stu-id="8be63-310">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="8be63-311">Bu nedenle, çıktı veri kümesinin 24 dilim hello ardışık düzen tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8be63-311">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="8be63-312">Adlı hello komutu toovariable Ata **cmd**.</span><span class="sxs-lookup"><span data-stu-id="8be63-312">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="8be63-313">Merhaba komutunu kullanarak çalıştırmak **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="8be63-313">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="8be63-314">Merhaba sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="8be63-314">View hello results.</span></span> <span data-ttu-id="8be63-315">Merhaba veri kümesi başarıyla oluşturuldu, hello JSON hello hello kümesinde için bkz: **sonuçları**; Aksi takdirde bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="8be63-315">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>  

    ```PowerShell   
    Write-Host $results
    ```

<span data-ttu-id="8be63-316">**Tebrikler!**</span><span class="sxs-lookup"><span data-stu-id="8be63-316">**Congratulations!**</span></span> <span data-ttu-id="8be63-317">Azure Blob Storage tooAzure SQL veritabanından verileri kopyalayan bir işlem hattı ile bir Azure data factory başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="8be63-317">You have successfully created an Azure data factory, with a pipeline that copies data from Azure Blob Storage tooAzure SQL database.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="8be63-318">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="8be63-318">Monitor pipeline</span></span>
<span data-ttu-id="8be63-319">Bu adımda, veri fabrikası REST API toomonitor dilimler hello ardışık düzen tarafından üretilen kullanın.</span><span class="sxs-lookup"><span data-stu-id="8be63-319">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> <span data-ttu-id="8be63-320">Merhaba başlangıç ve bitiş aşağıdaki belirtilen hello kez eşleşme hello başlangıç komut ve bitiş saatlerini hello ardışık emin olun.</span><span class="sxs-lookup"><span data-stu-id="8be63-320">Make sure that hello start and end times specified in hello following command match hello start and end times of hello pipeline.</span></span> 

```PowerShell
$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=2017-05-11T00%3a00%3a00.0000000Z"&"end=2017-05-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};
```

```PowerShell
$results2 = Invoke-Command -scriptblock $cmd;
```

```PowerShell
IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

<span data-ttu-id="8be63-321">Bir dilim görene kadar bir sonraki hello Invoke-Command ve hello çalıştıran **hazır** durumu veya **başarısız** durumu.</span><span class="sxs-lookup"><span data-stu-id="8be63-321">Run hello Invoke-Command and hello next one until you see a slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="8be63-322">Merhaba dilim hazır durumunda olduğunda hello denetleyin **emp** hello çıktı verileri için Azure SQL veritabanı tablosunda.</span><span class="sxs-lookup"><span data-stu-id="8be63-322">When hello slice is in Ready state, check hello **emp** table in your Azure SQL database for hello output data.</span></span> 

<span data-ttu-id="8be63-323">Her dilim için iki hello kaynak dosyadan veri satırı kopyalanan toohello emp tablosunda hello Azure SQL veritabanı ' dir.</span><span class="sxs-lookup"><span data-stu-id="8be63-323">For each slice, two rows of data from hello source file are copied toohello emp table in hello Azure SQL database.</span></span> <span data-ttu-id="8be63-324">Bu nedenle, tüm hello dilimleri (hazır durumda) başarıyla işlendiğinde hello emp tablosunda 24 yeni kayıtlar bakın.</span><span class="sxs-lookup"><span data-stu-id="8be63-324">Therefore, you see 24 new records in hello emp table when all hello slices are successfully processed (in Ready state).</span></span> 

## <a name="summary"></a><span data-ttu-id="8be63-325">Özet</span><span class="sxs-lookup"><span data-stu-id="8be63-325">Summary</span></span>
<span data-ttu-id="8be63-326">Bu öğreticide, REST API toocreate bir Azure veri fabrikası toocopy verileri Azure blob tooan Azure SQL veritabanından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8be63-326">In this tutorial, you used REST API toocreate an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="8be63-327">Bu öğreticide gerçekleştirilen hello üst düzey adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8be63-327">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="8be63-328">Oluşturulan Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="8be63-328">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="8be63-329">Oluşturulan **bağlı hizmetler**:</span><span class="sxs-lookup"><span data-stu-id="8be63-329">Created **linked services**:</span></span>
   1. <span data-ttu-id="8be63-330">Bir Azure depolama hizmeti toolink girdi verilerini tutan Azure Storage hesabınıza bağlı.</span><span class="sxs-lookup"><span data-stu-id="8be63-330">An Azure Storage linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="8be63-331">Bir Azure SQL Hizmeti toolink hello çıktı verilerini tutan Azure SQL veritabanınızı bağlı.</span><span class="sxs-lookup"><span data-stu-id="8be63-331">An Azure SQL linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="8be63-332">İşlem hatları için girdi ve çıktı verilerini açıklayan **veri kümeleri** oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="8be63-332">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="8be63-333">Kaynak olarak BlobSource’u, havuz olarak SqlSink’i kapsayan bir Kopyalama Etkinliği’ne sahip bir **işlem hattı** oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="8be63-333">Created a **pipeline** with a Copy Activity with BlobSource as source and SqlSink as sink.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8be63-334">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8be63-334">Next steps</span></span>
<span data-ttu-id="8be63-335">Bu öğreticide, bir kopyalama işleminde kaynak veri deposu olarak Azure blob depolama alanını ve hedef veri deposu olarak Azure SQL veritabanını kullandınız.</span><span class="sxs-lookup"><span data-stu-id="8be63-335">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="8be63-336">Merhaba aşağıdaki tabloda kaynakları ve hedefleri hello kopyalama etkinliği tarafından desteklenen veri depoları listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8be63-336">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="8be63-337">nasıl bir veri öğesine/öğesinden toocopy veri deposu hakkında toolearn hello veri deposu hello tablosundaki hello bağlantısını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="8be63-337">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
