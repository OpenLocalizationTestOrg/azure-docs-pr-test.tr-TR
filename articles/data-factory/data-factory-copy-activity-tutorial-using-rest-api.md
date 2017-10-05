---
title: "Öğretici: Azure Data Factory işlem hattı oluşturmak için REST API kullanma | Microsoft Docs"
description: "Bu öğreticide, Azure blob depolama alanından Azure SQL veritabanına veri kopyalamak için REST API kullanarak Kopyalama Etkinliği içeren Azure Data Factory işlem hattı oluşturursunuz."
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
ms.openlocfilehash: 6663774497aa18aa98e7e8c5aed6183c599b2172
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-use-rest-api-to-create-an-azure-data-factory-pipeline-to-copy-data"></a><span data-ttu-id="ff037-103">Öğretici: Verileri kopyalamak amacıyla Azure Data Factory işlem hattı oluşturmak için REST API kullanma</span><span class="sxs-lookup"><span data-stu-id="ff037-103">Tutorial: Use REST API to create an Azure Data Factory pipeline to copy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff037-104">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="ff037-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="ff037-105">Kopyalama Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="ff037-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="ff037-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ff037-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="ff037-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ff037-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="ff037-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff037-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="ff037-109">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="ff037-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="ff037-110">REST API</span><span class="sxs-lookup"><span data-stu-id="ff037-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="ff037-111">.NET API’si</span><span class="sxs-lookup"><span data-stu-id="ff037-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="ff037-112">Bu makalede, Azure blob depolama alanından Azure SQL veritabanına veri kopyalayan bir işlem hattıyla veri fabrikası oluşturmak için REST API’yi nasıl kullanacağınızı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="ff037-112">In this article, you learn how to use REST API to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="ff037-113">Azure Data Factory’yi ilk kez kullanıyorsanız bu öğreticiyi tamamlamadan önce [Azure Data Factory’ye Giriş](data-factory-introduction.md) makalesini okuyun.</span><span class="sxs-lookup"><span data-stu-id="ff037-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="ff037-114">Bu öğreticide, içinde bir etkinlik olan işlem hattı oluşturursunuz: Kopyalama Etkinliği.</span><span class="sxs-lookup"><span data-stu-id="ff037-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="ff037-115">Kopyalama etkinliği, verileri, desteklenen bir veri deposundan desteklenen bir havuz veri deposuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="ff037-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="ff037-116">Kaynak ve havuz olarak desteklenen veri depolarının listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="ff037-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="ff037-117">Etkinlik, çeşitli veri depolama alanları arasında güvenli, güvenilir ve ölçeklenebilir bir yolla veri kopyalayabilen genel olarak kullanılabilir bir hizmet tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="ff037-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="ff037-118">Kopyalama Etkinliği hakkında daha fazla bilgi için bkz. [Veri Taşıma Etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ff037-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="ff037-119">Bir işlem hattında birden fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="ff037-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="ff037-120">Bir etkinliğin çıkış veri kümesini diğer etkinliğin giriş veri kümesi olarak ayarlayarak iki etkinliği zincirleyebilir, yani bir etkinliğin diğerinden sonra çalıştırılmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff037-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="ff037-121">Daha fazla bilgi için bkz. [bir işlem hattında birden fazla etkinlik](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="ff037-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="ff037-122">Bu makale, Data Factory REST API’sinin tamamını kapsamaz.</span><span class="sxs-lookup"><span data-stu-id="ff037-122">This article does not cover all the Data Factory REST API.</span></span> <span data-ttu-id="ff037-123">Data Factory cmdlet’leri hakkında kapsamlı belgeler için bkz. [Data Factory REST API Başvurusu](/rest/api/datafactory/).</span><span class="sxs-lookup"><span data-stu-id="ff037-123">See [Data Factory REST API Reference](/rest/api/datafactory/) for comprehensive documentation on Data Factory cmdlets.</span></span>
>  
> <span data-ttu-id="ff037-124">Bu öğreticideki veri işlem hattı, bir kaynak veri deposundaki verileri hedef veri deposuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="ff037-124">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="ff037-125">Azure Data Factory kullanarak verileri dönüştürme hakkında bir öğretici için bkz. [Öğretici: Hadoop kümesi kullanarak verileri dönüştürmek için işlem hattı oluşturma](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="ff037-125">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff037-126">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ff037-126">Prerequisites</span></span>
* <span data-ttu-id="ff037-127">[Öğreticiye Genel Bakış](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) bölümünü inceleyin ve **ön koşul** adımlarını tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="ff037-127">Go through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="ff037-128">[Curl](https://curl.haxx.se/dlwiz/) aracını makinenize yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ff037-128">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="ff037-129">Bir veri fabrikası oluşturmak için Curl aracını REST komutlarıyla kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="ff037-129">You use the Curl tool with REST commands to create a data factory.</span></span> 
* <span data-ttu-id="ff037-130">Aşağıdakileri yapmak için [bu makaledeki](../azure-resource-manager/resource-group-create-service-principal-portal.md) yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="ff037-130">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span> 
  1. <span data-ttu-id="ff037-131">Azure Active Directory’de **ADFCopyTutorialApp** adlı bir Web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff037-131">Create a Web application named **ADFCopyTutorialApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="ff037-132">**İstemci kimliği** ve **gizli anahtarı** alın.</span><span class="sxs-lookup"><span data-stu-id="ff037-132">Get **client ID** and **secret key**.</span></span> 
  3. <span data-ttu-id="ff037-133">**İstemci kimliğini** alın.</span><span class="sxs-lookup"><span data-stu-id="ff037-133">Get **tenant ID**.</span></span> 
  4. <span data-ttu-id="ff037-134">**ADFCopyTutorialApp** uygulamasını **Data Factory Katılımcısı** rolüne atayın.</span><span class="sxs-lookup"><span data-stu-id="ff037-134">Assign the **ADFCopyTutorialApp** application to the **Data Factory Contributor** role.</span></span>  
* <span data-ttu-id="ff037-135">[Azure PowerShell](/powershell/azure/overview)'i yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ff037-135">Install [Azure PowerShell](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="ff037-136">**PowerShell**’i başlatın ve aşağıdaki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="ff037-136">Launch **PowerShell** and do the following steps.</span></span> <span data-ttu-id="ff037-137">Bu öğreticide sonuna kadar Azure PowerShell’i açık tutun.</span><span class="sxs-lookup"><span data-stu-id="ff037-137">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="ff037-138">Kapatıp yeniden açarsanız komutları yeniden çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff037-138">If you close and reopen, you need to run the commands again.</span></span>
  
  1. <span data-ttu-id="ff037-139">Aşağıdaki komutu çalıştırın ve Azure portalda oturum açmak için kullandığınız kullanıcı adı ve parolayı girin:</span><span class="sxs-lookup"><span data-stu-id="ff037-139">Run the following command and enter the user name and password that you use to sign in to the Azure portal:</span></span>
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. <span data-ttu-id="ff037-140">Bu hesapla ilgili tüm abonelikleri görmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ff037-140">Run the following command to view all the subscriptions for this account:</span></span>

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. <span data-ttu-id="ff037-141">Çalışmak isteğiniz aboneliği seçmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ff037-141">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="ff037-142">**&lt;NameOfAzureSubscription**&gt; değerini Azure aboneliğinizin adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ff037-142">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span> 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. <span data-ttu-id="ff037-143">PowerShell’de aşağıdaki komutu çalıştırarak **ADFTutorialResourceGroup** adlı bir Azure kaynak grubu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ff037-143">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell:</span></span>  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      <span data-ttu-id="ff037-144">Kaynak grubu zaten varsa bunun güncelleştirileceğini mi (Y) yoksa (N) olarak tutulacağını mı belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff037-144">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span> 
     
      <span data-ttu-id="ff037-145">Bu öğreticideki adımlardan bazıları ADFTutorialResourceGroup adlı kaynak grubunu kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="ff037-145">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="ff037-146">Farklı bir kaynak grubu kullanıyorsanız, bu öğreticide kullanılan ADFTutorialResourceGroup yerine kaynak grubunuzun adını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff037-146">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="ff037-147">JSON tanımları oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff037-147">Create JSON definitions</span></span>
<span data-ttu-id="ff037-148">Curl.exe’nin bulunduğu klasörde aşağıdaki JSON dosyalarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff037-148">Create following JSON files in the folder where curl.exe is located.</span></span> 

### <a name="datafactoryjson"></a><span data-ttu-id="ff037-149">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="ff037-149">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ff037-150">Adın genel olarak benzersiz olması gerektiğinden, ADFCopyTutorialDF’yi benzersiz bir ada dönüştürmek için önüne/sonuna bir şeyler eklemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff037-150">Name must be globally unique, so you may want to prefix/suffix ADFCopyTutorialDF to make it a unique name.</span></span> 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="ff037-151">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="ff037-151">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ff037-152">**accountname** ve **accountkey** sözcüklerini Azure depolama hesabınızın adı ve anahtarıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ff037-152">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="ff037-153">Depolama erişim anahtarınızı nasıl alacağınız hakkında bilgi için bkz. [Depolama erişim anahtarlarını görüntüleme, kopyalama ve yeniden oluşturma](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="ff037-153">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>

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

<span data-ttu-id="ff037-154">JSON özellikleri hakkındaki ayrıntılar için bkz. [Azure Depolama bağlı hizmeti](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="ff037-154">For details about JSON properties, see [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span></span>

### <a name="azuersqllinkedservicejson"></a><span data-ttu-id="ff037-155">azuersqllinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="ff037-155">azuersqllinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ff037-156">**servername**, **databasename**, **username** ve **password** sözcüklerini Azure SQL sunucunuzun adı, SQL veritabanınızın adı, kullanıcı hesabınız ve hesap parolanızla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ff037-156">Replace **servername**, **databasename**, **username**, and **password** with name of your Azure SQL server, name of SQL database, user account, and password for the account.</span></span>  
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

<span data-ttu-id="ff037-157">JSON özellikleri hakkındaki ayrıntılar için bkz. [Azure SQL bağlı hizmeti](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ff037-157">For details about JSON properties, see [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="ff037-158">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="ff037-158">inputdataset.json</span></span>

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

<span data-ttu-id="ff037-159">Aşağıdaki tabloda, kod parçacığında kullanılan JSON özellikleri için açıklamalar verilmektedir:</span><span class="sxs-lookup"><span data-stu-id="ff037-159">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="ff037-160">Özellik</span><span class="sxs-lookup"><span data-stu-id="ff037-160">Property</span></span> | <span data-ttu-id="ff037-161">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff037-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ff037-162">type</span><span class="sxs-lookup"><span data-stu-id="ff037-162">type</span></span> | <span data-ttu-id="ff037-163">Veriler Azure blob depolama alanında yer aldığından type özelliği **AzureBlob** olarak ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ff037-163">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
| <span data-ttu-id="ff037-164">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="ff037-164">linkedServiceName</span></span> | <span data-ttu-id="ff037-165">Daha önce oluşturduğunuz **AzureStorageLinkedService**’e başvurur.</span><span class="sxs-lookup"><span data-stu-id="ff037-165">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="ff037-166">folderPath</span><span class="sxs-lookup"><span data-stu-id="ff037-166">folderPath</span></span> | <span data-ttu-id="ff037-167">blob **kapsayıcıyı** ve girdi blob’larını içeren **klasörü** belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff037-167">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="ff037-168">Bu öğreticide adftutorial, blob kapsayıcısıdır ve klasör, kök klasördür.</span><span class="sxs-lookup"><span data-stu-id="ff037-168">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
| <span data-ttu-id="ff037-169">fileName</span><span class="sxs-lookup"><span data-stu-id="ff037-169">fileName</span></span> | <span data-ttu-id="ff037-170">Bu özellik isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ff037-170">This property is optional.</span></span> <span data-ttu-id="ff037-171">Bu özelliği atarsanız tüm folderPath dosyaları alınır.</span><span class="sxs-lookup"><span data-stu-id="ff037-171">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="ff037-172">Bu öğreticide fileName için **emp.txt** belirtilir, bu nedenle işlem için yalnızca bu dosya seçilir.</span><span class="sxs-lookup"><span data-stu-id="ff037-172">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
| <span data-ttu-id="ff037-173">format -> type</span><span class="sxs-lookup"><span data-stu-id="ff037-173">format -> type</span></span> |<span data-ttu-id="ff037-174">Girdi dosyası metin biçiminde olduğundan **TextFormat**'ı kullanırız.</span><span class="sxs-lookup"><span data-stu-id="ff037-174">The input file is in the text format, so we use **TextFormat**.</span></span> |
| <span data-ttu-id="ff037-175">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="ff037-175">columnDelimiter</span></span> | <span data-ttu-id="ff037-176">Girdi dosyasındaki sütunlar, **virgül (`,`)** ile ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="ff037-176">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
| <span data-ttu-id="ff037-177">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="ff037-177">frequency/interval</span></span> | <span data-ttu-id="ff037-178">frequency **Saat**, interval da **1** olarak ayarlanmıştır. Bu, girdi dilimlerinin **saatlik** olarak kullanılabileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff037-178">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="ff037-179">Başka bir deyişle, Data Factory hizmeti belirttiğiniz blob kapsayıcısının (**adftutorial**) kök klasöründe girdi verilerini saatte bir kere arar.</span><span class="sxs-lookup"><span data-stu-id="ff037-179">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="ff037-180">İşlem hattı başlangıç ve bitiş zamanlarındaki verileri arar, bu zamanlardan önceki veya sonraki verileri aramaz.</span><span class="sxs-lookup"><span data-stu-id="ff037-180">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
| <span data-ttu-id="ff037-181">external</span><span class="sxs-lookup"><span data-stu-id="ff037-181">external</span></span> | <span data-ttu-id="ff037-182">Bu özellik, veriler bu işlem hattı tarafından oluşturulmazsa **true** olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="ff037-182">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="ff037-183">Bu öğreticideki girdi verileri, bu işlem hattı tarafından oluşturulmayan emp.txt dosyasında bulunur, bu nedenle bu özelliği true olarak ayarlarız.</span><span class="sxs-lookup"><span data-stu-id="ff037-183">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

<span data-ttu-id="ff037-184">Bu JSON özellikleri hakkında daha fazla bilgi için bkz. [Azure Blob bağlayıcısı makalesi](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ff037-184">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>

### <a name="outputdatasetjson"></a><span data-ttu-id="ff037-185">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="ff037-185">outputdataset.json</span></span>

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
<span data-ttu-id="ff037-186">Aşağıdaki tabloda, kod parçacığında kullanılan JSON özellikleri için açıklamalar verilmektedir:</span><span class="sxs-lookup"><span data-stu-id="ff037-186">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="ff037-187">Özellik</span><span class="sxs-lookup"><span data-stu-id="ff037-187">Property</span></span> | <span data-ttu-id="ff037-188">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ff037-188">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ff037-189">type</span><span class="sxs-lookup"><span data-stu-id="ff037-189">type</span></span> | <span data-ttu-id="ff037-190">type özelliği, veriler Azure SQL veritabanındaki bir tabloya kopyalandığından **AzureSqlTable** olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="ff037-190">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
| <span data-ttu-id="ff037-191">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="ff037-191">linkedServiceName</span></span> | <span data-ttu-id="ff037-192">Daha önce oluşturduğunuz **AzureSqlLinkedService**’e başvurur.</span><span class="sxs-lookup"><span data-stu-id="ff037-192">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="ff037-193">tableName</span><span class="sxs-lookup"><span data-stu-id="ff037-193">tableName</span></span> | <span data-ttu-id="ff037-194">Verilerin kopyalandığı **tabloyu** belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff037-194">Specified the **table** to which the data is copied.</span></span> | 
| <span data-ttu-id="ff037-195">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="ff037-195">frequency/interval</span></span> | <span data-ttu-id="ff037-196">frequency **Saatlik** ve interval **1** olarak ayarlanır. Bu durumda çıktı dilimleri, işlem hattı başlangıç ve bitiş zamanları arasında **saatlik** olarak üretilir, bu zamanlardan önce veya sonra üretilmez.</span><span class="sxs-lookup"><span data-stu-id="ff037-196">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

<span data-ttu-id="ff037-197">Veritabanındaki emp tablosunda üç sütun vardır: **ID**, **FirstName** ve **LastName**.</span><span class="sxs-lookup"><span data-stu-id="ff037-197">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="ff037-198">ID bir kimlik sütunu olduğundan, burada yalnızca **FirstName** ve **LastName** değerlerini belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff037-198">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

<span data-ttu-id="ff037-199">Bu JSON özellikleri hakkında daha fazla bilgi için bkz. [Azure SQL bağlayıcısı makalesi](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ff037-199">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="ff037-200">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="ff037-200">pipeline.json</span></span>

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob to Azure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data to Azure SQL database",
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

<span data-ttu-id="ff037-201">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="ff037-201">Note the following points:</span></span>

- <span data-ttu-id="ff037-202">Etkinlikler bölümünde, **türü** **Copy** olarak ayarlanmış yalnızca bir etkinlik vardır.</span><span class="sxs-lookup"><span data-stu-id="ff037-202">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="ff037-203">Kopyalama etkinliği hakkında daha fazla bilgi için bkz. [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ff037-203">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="ff037-204">Data Factory çözümlerinde, [veri dönüştürme etkinliklerini](data-factory-data-transformation-activities.md) de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff037-204">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
- <span data-ttu-id="ff037-205">Etkinlik girdisi **AzureBlobInput** olarak, etkinlik çıktısıysa **AzureSqlOutput** olarak ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ff037-205">Input for the activity is set to **AzureBlobInput** and output for the activity is set to **AzureSqlOutput**.</span></span> 
- <span data-ttu-id="ff037-206">**typeProperties** bölümünde **BlobSource** kaynak türü, **SqlSink** de havuz türü olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="ff037-206">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="ff037-207">Kaynak ve havuz olarak kopyalama etkinliği tarafından desteklenen veri depolarının eksiksiz listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="ff037-207">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="ff037-208">Kaynak/havuz olarak desteklenen belirli bir veri deposunu nasıl kullanacağınızı öğrenmek için tablodaki bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ff037-208">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
 
<span data-ttu-id="ff037-209">**start** özelliğinin değerini geçerli günle, **end** değerini de sonraki günle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ff037-209">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="ff037-210">Tarih saatin yalnızca tarih bölümünü belirtip saat bölümünü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff037-210">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="ff037-211">Örneğin, "2017-02-03", "2017-02-03T00:00:00Z" ile eşdeğerdir</span><span class="sxs-lookup"><span data-stu-id="ff037-211">For example, "2017-02-03", which is equivalent to "2017-02-03T00:00:00Z"</span></span>
 
<span data-ttu-id="ff037-212">Başlangıç ve bitiş tarih saatleri [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff037-212">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="ff037-213">Örneğin: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="ff037-213">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="ff037-214">**End** zamanı isteğe bağlıdır; ancak bu öğreticide bunu kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="ff037-214">The **end** time is optional, but we use it in this tutorial.</span></span> 
 
<span data-ttu-id="ff037-215">**end** özelliği için değer belirtmezseniz "**start + 48 hours**" olarak hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="ff037-215">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="ff037-216">İşlem hattını süresiz olarak çalıştırmak için **end** özelliği değerini **9999-09-09** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ff037-216">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
 
<span data-ttu-id="ff037-217">Önceki örnekte, her veri dilimi saatlik oluşturulduğundan 24 veri dilimi vardır.</span><span class="sxs-lookup"><span data-stu-id="ff037-217">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

<span data-ttu-id="ff037-218">İşlem hattı tanımındaki JSON özelliklerinin açıklamaları için [işlem hatları oluşturma](data-factory-create-pipelines.md) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="ff037-218">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ff037-219">Kopyalama etkinliği tanımındaki JSON özelliklerinin açıklamaları için bkz. [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ff037-219">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="ff037-220">BlobSource tarafından desteklenen JSON özelliklerinin açıklamaları için bkz. [Azure Blob bağlayıcısı makalesi](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="ff037-220">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="ff037-221">SqlSink tarafından desteklenen JSON özelliklerinin açıklamaları için bkz. [Azure SQL Veritabanı bağlayıcısı makalesi](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="ff037-221">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="set-global-variables"></a><span data-ttu-id="ff037-222">Genel değişkenleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="ff037-222">Set global variables</span></span>
<span data-ttu-id="ff037-223">Azure PowerShell’de değerleri kendi değerlerinizle değiştirdikten sonra aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ff037-223">In Azure PowerShell, execute the following commands after replacing the values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff037-224">İstemci kimliği, istemci parolası, kiracı kimliği ve abonelik kimliğini edinme konusunda yönergeler için [Önkoşullar](#prerequisites) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="ff037-224">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

<span data-ttu-id="ff037-225">Kullanmakta olduğunuz veri fabrikasının adını güncelleştirdikten sonra aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ff037-225">Run the following command after updating the name of the data factory you are using:</span></span> 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a><span data-ttu-id="ff037-226">AAD ile kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="ff037-226">Authenticate with AAD</span></span>
<span data-ttu-id="ff037-227">Azure Active Directory (AAD) ile kimlik doğrulamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ff037-227">Run the following command to authenticate with Azure Active Directory (AAD):</span></span> 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a><span data-ttu-id="ff037-228">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff037-228">Create data factory</span></span>
<span data-ttu-id="ff037-229">Bu adımda, **ADFCopyTutorialDF** adlı bir Azure Data Factory oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ff037-229">In this step, you create an Azure Data Factory named **ADFCopyTutorialDF**.</span></span> <span data-ttu-id="ff037-230">Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ff037-230">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="ff037-231">İşlem hattında bir veya daha fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="ff037-231">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="ff037-232">Örneğin, bir kaynaktan hedef veri depolama alanına veri kopyalamak için bir Kopyalama Etkinliği.</span><span class="sxs-lookup"><span data-stu-id="ff037-232">For example, a Copy Activity to copy data from a source to a destination data store.</span></span> <span data-ttu-id="ff037-233">Giriş verilerini ürün çıktı verilerine dönüştürmek için bir Hive betiği çalıştırmak üzere kullanılan bir HDInsight Hive etkinliği.</span><span class="sxs-lookup"><span data-stu-id="ff037-233">A HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="ff037-234">Veri fabrikasını oluşturmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ff037-234">Run the following commands to create the data factory:</span></span> 

1. <span data-ttu-id="ff037-235">Komutu **cmd** adlı değişkene atayın.</span><span class="sxs-lookup"><span data-stu-id="ff037-235">Assign the command to variable named **cmd**.</span></span> 
   
    > [!IMPORTANT]
    > <span data-ttu-id="ff037-236">Burada belirttiğiniz veri fabrikasının (ADFCopyTutorialDF) adının **datafactory.json**’da belirtilen adla eşleştiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ff037-236">Confirm that the name of the data factory you specify here (ADFCopyTutorialDF) matches the name specified in the **datafactory.json**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. <span data-ttu-id="ff037-237">**Invoke-Command** komutunu kullanarak komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ff037-237">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="ff037-238">Sonuçlara bakın.</span><span class="sxs-lookup"><span data-stu-id="ff037-238">View the results.</span></span> <span data-ttu-id="ff037-239">Veri fabrikası başarıyla oluşturulduysa, **results** bölümünde veri fabrikasının JSON’unu görürsünüz; aksi takdirde bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ff037-239">If the data factory has been successfully created, you see the JSON for the data factory in the **results**; otherwise, you see an error message.</span></span>  
   
    ```
    Write-Host $results
    ```

<span data-ttu-id="ff037-240">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="ff037-240">Note the following points:</span></span>

* <span data-ttu-id="ff037-241">Azure Data Factory adı küresel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ff037-241">The name of the Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="ff037-242">Sonuçlarda **Veri fabrikası adı “ADFCopyTutorialDF” kullanılamıyor** hatasını görürseniz aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="ff037-242">If you see the error in results: **Data factory name “ADFCopyTutorialDF” is not available**, do the following steps:</span></span>  
  
  1. <span data-ttu-id="ff037-243">**datafactory.json** dosyasında adı değiştirin (örneğin, adınızADFCopyTutorialDF).</span><span class="sxs-lookup"><span data-stu-id="ff037-243">Change the name (for example, yournameADFCopyTutorialDF) in the **datafactory.json** file.</span></span>
  2. <span data-ttu-id="ff037-244">**$cmd** değişkenine bir değerin atandığı ilk komutta, ADFCopyTutorialDF’yi yeni adla değiştirip komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ff037-244">In the first command where the **$cmd** variable is assigned a value, replace ADFCopyTutorialDF with the new name and run the command.</span></span> 
  3. <span data-ttu-id="ff037-245">Veri fabrikasını oluşturmak ve işlemin sonuçlarını yazdırmak üzere REST API’yi çağırmak için sonraki iki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ff037-245">Run the next two commands to invoke the REST API to create the data factory and print the results of the operation.</span></span> 
     
     <span data-ttu-id="ff037-246">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="ff037-246">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="ff037-247">Data Factory örnekleri oluşturmak için, Azure aboneliğinde katılımcı/yönetici rolünüz olmalıdır</span><span class="sxs-lookup"><span data-stu-id="ff037-247">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span></span>
* <span data-ttu-id="ff037-248">Veri fabrikasının adı gelecekte bir DNS adı olarak kaydedilmiş ve herkese görünür hale gelmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="ff037-248">The name of the data factory may be registered as a DNS name in the future and hence become publicly visible.</span></span>
* <span data-ttu-id="ff037-249">Şu hatayı alırsanız: "**Abonelik, Microsoft.DataFactory ad alanını kullanacak şekilde kaydedilmemiş**", aşağıdakilerden birini yapın ve yeniden yayımlamayı deneyin:</span><span class="sxs-lookup"><span data-stu-id="ff037-249">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span></span> 
  
  * <span data-ttu-id="ff037-250">Azure PowerShell’de Data Factory sağlayıcısını kaydetmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ff037-250">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="ff037-251">Data Factory sağlayıcısının kayıtlı olduğunu onaylamak için aşağıdaki komutu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff037-251">You can run the following command to confirm that the Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="ff037-252">Azure aboneliğini kullanarak [Azure portalında](https://portal.azure.com) oturum açın ve Data Factory dikey penceresine gidin (ya da) Azure portalında bir data factory oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff037-252">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="ff037-253">Bu eylem sağlayıcıyı sizin için otomatik olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ff037-253">This action automatically registers the provider for you.</span></span>

<span data-ttu-id="ff037-254">İşlem hattı oluşturmadan önce, öncelikle birkaç Data Factory varlığı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff037-254">Before creating a pipeline, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="ff037-255">İlk olarak kaynak ve hedef veri depolarını kendi veri deponuza bağlamak için bağlı hizmetler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff037-255">You first create linked services to link source and destination data stores to your data store.</span></span> <span data-ttu-id="ff037-256">Daha sonra, bağlı veri depolarındaki verileri temsil eden girdi ve çıktı veri kümeleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ff037-256">Then, define input and output datasets to represent data in linked data stores.</span></span> <span data-ttu-id="ff037-257">Son olarak bu veri kümelerini kullanan bir etkinlik ile işlem hattını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff037-257">Finally, create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="ff037-258">Bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff037-258">Create linked services</span></span>
<span data-ttu-id="ff037-259">Veri depolarınızı ve işlem hizmetlerinizi veri fabrikasına bağlamak için veri fabrikasında bağlı hizmetler oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="ff037-259">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="ff037-260">Bu öğreticide, Azure HDInsight veya Azure Data Lake Analytics gibi herhangi bir işlem hizmeti kullanmazsınız.</span><span class="sxs-lookup"><span data-stu-id="ff037-260">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="ff037-261">Azure Depolama (kaynak) ve Azure SQL Veritabanı (hedef) türünde iki veri deposu kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="ff037-261">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> <span data-ttu-id="ff037-262">Bu nedenle, AzureStorage ve AzureSqlDatabase türlerinde AzureStorageLinkedService ve AzureSqlLinkedService adlı iki bağlı hizmet oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="ff037-262">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="ff037-263">AzureStorageLinkedService, Azure depolama hesabınızı veri fabrikasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="ff037-263">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="ff037-264">Bu depolama hesabı, kapsayıcı oluşturduğunuz ve verileri [ön koşulların](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) parçası olarak yüklediğiniz hesaptır.</span><span class="sxs-lookup"><span data-stu-id="ff037-264">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="ff037-265">AzureSqlLinkedService, Azure SQL veritabanınızı veri fabrikasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="ff037-265">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="ff037-266">Blob depolama alanından kopyalanan veriler bu veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="ff037-266">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="ff037-267">Bu veritabanındaki emp tablosunu, [ön koşulların](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) parçası olarak oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="ff037-267">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="ff037-268">Azure Storage bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff037-268">Create Azure Storage linked service</span></span>
<span data-ttu-id="ff037-269">Bu adımda, Azure depolama hesabınızı veri fabrikanıza bağlarsınız.</span><span class="sxs-lookup"><span data-stu-id="ff037-269">In this step, you link your Azure storage account to your data factory.</span></span> <span data-ttu-id="ff037-270">Bu bölümde Azure depolama hesabınızın adını ve anahtarını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff037-270">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="ff037-271">Bir Azure Storage bağlı hizmetini tanımlamak için kullanılan JSON özelliklerine ilişkin ayrıntılar için bkz. [Azure Storage bağlı hizmeti](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="ff037-271">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span>  

1. <span data-ttu-id="ff037-272">Komutu **cmd** adlı değişkene atayın.</span><span class="sxs-lookup"><span data-stu-id="ff037-272">Assign the command to variable named **cmd**.</span></span> 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="ff037-273">**Invoke-Command** komutunu kullanarak komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ff037-273">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="ff037-274">Sonuçlara bakın.</span><span class="sxs-lookup"><span data-stu-id="ff037-274">View the results.</span></span> <span data-ttu-id="ff037-275">Bağlı hizmet başarıyla oluşturulduysa, **results** bölümünde bağlı hizmetin JSON’unu görürsünüz; aksi takdirde bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ff037-275">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a><span data-ttu-id="ff037-276">Azure SQL bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff037-276">Create Azure SQL linked service</span></span>
<span data-ttu-id="ff037-277">Bu adımda, Azure SQL veritabanınızı veri fabrikanıza bağlarsınız.</span><span class="sxs-lookup"><span data-stu-id="ff037-277">In this step, you link your Azure SQL database to your data factory.</span></span> <span data-ttu-id="ff037-278">Bu bölümde Azure SQL sunucu adı, veritabanı adı, kullanıcı adı ve kullanıcı parolasını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff037-278">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="ff037-279">Bir Azure SQL bağlı hizmetini tanımlamak için kullanılan JSON özelliklerine ilişkin ayrıntılar için bkz. [Azure SQL bağlı hizmeti](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ff037-279">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used to define an Azure SQL linked service.</span></span>

1. <span data-ttu-id="ff037-280">Komutu **cmd** adlı değişkene atayın.</span><span class="sxs-lookup"><span data-stu-id="ff037-280">Assign the command to variable named **cmd**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="ff037-281">**Invoke-Command** komutunu kullanarak komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ff037-281">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="ff037-282">Sonuçlara bakın.</span><span class="sxs-lookup"><span data-stu-id="ff037-282">View the results.</span></span> <span data-ttu-id="ff037-283">Bağlı hizmet başarıyla oluşturulduysa, **results** bölümünde bağlı hizmetin JSON’unu görürsünüz; aksi takdirde bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ff037-283">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="ff037-284">Veri kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff037-284">Create datasets</span></span>
<span data-ttu-id="ff037-285">Önceki adımda, Azure Depolama hesabınızı ve Azure SQL veritabanınızı veri fabrikanıza bağlamak için bağlı hizmetler oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="ff037-285">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="ff037-286">Bu adımda, AzureBlobInput ve AzureSqlOutput adlı iki veri kümesi tanımlarsınız. Bu veri kümeleri, sırasıyla AzureStorageLinkedService ve AzureSqlLinkedService tarafından başvurulan veri depolarında depolanan girdi ve çıktı verilerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ff037-286">In this step, you define two datasets named AzureBlobInput and AzureSqlOutput that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="ff037-287">Azure depolama bağlı hizmeti, Data Factory hizmetinin Azure depolama hesabınıza bağlanmak için çalışma zamanında kullandığı bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff037-287">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="ff037-288">Giriş blob veri kümesi (AzureBlobInput) ise kapsayıcıyı ve girdi verilerini içeren klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff037-288">And, the input blob dataset (AzureBlobInput) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="ff037-289">Benzer şekilde Azure SQL Veritabanı bağlı hizmeti, Data Factory hizmetinin Azure SQL veritabanınıza bağlanmak için çalışma zamanında kullandığı bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff037-289">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="ff037-290">Çıktı SQL tablosu veri kümesi (OutputDataset) ise blob depolama alanındaki verilerin kopyalandığı veritabanında tabloyu belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff037-290">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="ff037-291">Girdi veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff037-291">Create input dataset</span></span>
<span data-ttu-id="ff037-292">Bu adımda, AzureBlobInput adlı bir veri kümesi oluşturursunuz. Bu veri kümesi, AzureStorageLinkedService bağlı hizmetiyle temsil edilen Azure Depolama’daki bir blob kapsayıcısının (adftutorial) kök klasöründe bulunan blob dosyasını (emp.txt) işaret eder.</span><span class="sxs-lookup"><span data-stu-id="ff037-292">In this step, you create a dataset named AzureBlobInput that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="ff037-293">fileName için bir değer belirtmezseniz (veya bu adımı atlarsanız) girdi klasöründe bulunan tüm blob’lardaki veriler hedefe kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="ff037-293">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="ff037-294">Bu öğreticide, fileName için bir değer belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff037-294">In this tutorial, you specify a value for the fileName.</span></span> 

1. <span data-ttu-id="ff037-295">Komutu **cmd** adlı değişkene atayın.</span><span class="sxs-lookup"><span data-stu-id="ff037-295">Assign the command to variable named **cmd**.</span></span> 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="ff037-296">**Invoke-Command** komutunu kullanarak komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ff037-296">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="ff037-297">Sonuçlara bakın.</span><span class="sxs-lookup"><span data-stu-id="ff037-297">View the results.</span></span> <span data-ttu-id="ff037-298">Veri kümesi başarıyla oluşturulduysa, **results** bölümünde veri kümesinin JSON’unu görürsünüz; aksi takdirde bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ff037-298">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="ff037-299">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff037-299">Create output dataset</span></span>
<span data-ttu-id="ff037-300">Azure SQL Veritabanı bağlı hizmeti, Data Factory hizmetinin Azure SQL veritabanınıza bağlanmak için çalışma zamanında kullandığı bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff037-300">The Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="ff037-301">Bu adımda oluşturduğunuz çıktı SQL tablosu veri kümesi (OutputDataset), blob depolama alanındaki verilerin kopyalandığı veritabanında tabloyu belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff037-301">The output SQL table dataset (OututDataset) you create in this step specifies the table in the database to which the data from the blob storage is copied.</span></span>

1. <span data-ttu-id="ff037-302">Komutu **cmd** adlı değişkene atayın.</span><span class="sxs-lookup"><span data-stu-id="ff037-302">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="ff037-303">**Invoke-Command** komutunu kullanarak komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ff037-303">Run the command by using **Invoke-Command**.</span></span>
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="ff037-304">Sonuçlara bakın.</span><span class="sxs-lookup"><span data-stu-id="ff037-304">View the results.</span></span> <span data-ttu-id="ff037-305">Veri kümesi başarıyla oluşturulduysa, **results** bölümünde veri kümesinin JSON’unu görürsünüz; aksi takdirde bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ff037-305">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a><span data-ttu-id="ff037-306">İşlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff037-306">Create pipeline</span></span>
<span data-ttu-id="ff037-307">Bu adımda, girdi olarak **AzureBlobInput**, çıktı olaraksa **AzureSqlOutput** kullanan bir **kopyalama etkinliğine** sahip bir işlem hattı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="ff037-307">In this step, you create a pipeline with a **copy activity** that uses **AzureBlobInput** as an input and **AzureSqlOutput** as an output.</span></span>

<span data-ttu-id="ff037-308">Şu anda zamanlamayı çıktı veri kümesi yürütmektedir.</span><span class="sxs-lookup"><span data-stu-id="ff037-308">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="ff037-309">Bu öğreticide, çıktı veri kümesi saatte bir dilim oluşturacak şekilde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="ff037-309">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="ff037-310">İşlem hattının başlangıç zamanı ve bitiş zamanı arasında bir gün, yani 24 saat vardır.</span><span class="sxs-lookup"><span data-stu-id="ff037-310">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="ff037-311">Bu nedenle işlem hattı, çıktı veri kümesinden 24 dilim oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff037-311">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 

1. <span data-ttu-id="ff037-312">Komutu **cmd** adlı değişkene atayın.</span><span class="sxs-lookup"><span data-stu-id="ff037-312">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="ff037-313">**Invoke-Command** komutunu kullanarak komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ff037-313">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="ff037-314">Sonuçlara bakın.</span><span class="sxs-lookup"><span data-stu-id="ff037-314">View the results.</span></span> <span data-ttu-id="ff037-315">Veri kümesi başarıyla oluşturulduysa, **results** bölümünde veri kümesinin JSON’unu görürsünüz; aksi takdirde bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ff037-315">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>  

    ```PowerShell   
    Write-Host $results
    ```

<span data-ttu-id="ff037-316">**Tebrikler!**</span><span class="sxs-lookup"><span data-stu-id="ff037-316">**Congratulations!**</span></span> <span data-ttu-id="ff037-317">Azure Blob Depolama’dan Azure SQL veritabanına veri kopyalayan bir işlem hattına sahip bir Azure veri fabrikasını başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="ff037-317">You have successfully created an Azure data factory, with a pipeline that copies data from Azure Blob Storage to Azure SQL database.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="ff037-318">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="ff037-318">Monitor pipeline</span></span>
<span data-ttu-id="ff037-319">Bu adımda, Data Factory REST API’sini kullanarak işlem hattı tarafından üretilmekte olan dilimleri izlersiniz.</span><span class="sxs-lookup"><span data-stu-id="ff037-319">In this step, you use Data Factory REST API to monitor slices being produced by the pipeline.</span></span>

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> <span data-ttu-id="ff037-320">Aşağıdaki komutta belirtilen başlangıç ve bitiş zamanlarının, işlem hattının başlangıç ve bitiş zamanlarıyla eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="ff037-320">Make sure that the start and end times specified in the following command match the start and end times of the pipeline.</span></span> 

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

<span data-ttu-id="ff037-321">Bir dilimi **Hazır** veya **Başarısız** durumunda görene kadar Invoke komutunu ve sonraki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ff037-321">Run the Invoke-Command and the next one until you see a slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="ff037-322">Dilim Ready durumundayken Azure SQL veritabanınızdaki **emp** tablosunda çıktı verileri olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="ff037-322">When the slice is in Ready state, check the **emp** table in your Azure SQL database for the output data.</span></span> 

<span data-ttu-id="ff037-323">Her dilim için kaynak dosyasından Azure SQL veritabanındaki emp tablosuna iki satır veri kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="ff037-323">For each slice, two rows of data from the source file are copied to the emp table in the Azure SQL database.</span></span> <span data-ttu-id="ff037-324">Bu nedenle, tüm dilimler başarıyla işlendiğinde (Ready durumunda) emp tablosunda 24 yeni kayıt görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ff037-324">Therefore, you see 24 new records in the emp table when all the slices are successfully processed (in Ready state).</span></span> 

## <a name="summary"></a><span data-ttu-id="ff037-325">Özet</span><span class="sxs-lookup"><span data-stu-id="ff037-325">Summary</span></span>
<span data-ttu-id="ff037-326">Bu öğreticide bir Azure blob’undan Azure SQL veritabanına veri kopyalamak için REST API kullanarak bir Azure veri fabrikası oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="ff037-326">In this tutorial, you used REST API to create an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="ff037-327">Bu öğreticide gerçekleştirilen üst düzey adımları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ff037-327">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="ff037-328">Azure **data factory** oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="ff037-328">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="ff037-329">Oluşturulan **bağlı hizmetler**:</span><span class="sxs-lookup"><span data-stu-id="ff037-329">Created **linked services**:</span></span>
   1. <span data-ttu-id="ff037-330">Girdi verilerinizi barındıran Azure Depolama hesabınızı bağlamak için bir Azure Depolama bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="ff037-330">An Azure Storage linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="ff037-331">Çıktı verilerinizi barındıran Azure SQL veritabanınızı bağlamak için bir Azure SQL bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="ff037-331">An Azure SQL linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="ff037-332">İşlem hatları için girdi ve çıktı verilerini açıklayan **veri kümeleri** oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="ff037-332">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="ff037-333">Kaynak olarak BlobSource’u, havuz olarak SqlSink’i kapsayan bir Kopyalama Etkinliği’ne sahip bir **işlem hattı** oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="ff037-333">Created a **pipeline** with a Copy Activity with BlobSource as source and SqlSink as sink.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ff037-334">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ff037-334">Next steps</span></span>
<span data-ttu-id="ff037-335">Bu öğreticide, bir kopyalama işleminde kaynak veri deposu olarak Azure blob depolama alanını ve hedef veri deposu olarak Azure SQL veritabanını kullandınız.</span><span class="sxs-lookup"><span data-stu-id="ff037-335">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="ff037-336">Aşağıdaki tabloda, kopyalama etkinliği tarafından kaynak ve hedef olarak desteklenen veri depolarının listesi sağlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="ff037-336">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="ff037-337">Veri deposundan/veri deposuna veri kopyalama hakkında bilgi edinmek için tablodaki veri deposunun bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ff037-337">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>