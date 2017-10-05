---
title: "SQL Server gelen ve veri taşıma | Microsoft Docs"
description: "Azure Data Factory kullanarak Azure VM'deki veya şirket içi SQL Server veritabanı için/gelen verileri taşıma hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: 9cd2077d897631457925cda5ef5e6df3c0c33177
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="fdc00-103">Azure Data Factory kullanarak verileri ve SQL Server şirket içi veya Iaas (Azure VM) üzerinde taşıma</span><span class="sxs-lookup"><span data-stu-id="fdc00-103">Move data to and from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="fdc00-104">Bu makalede kopya etkinliği Azure Data Factory'de bir şirket içi SQL Server veritabanından/gelen verileri taşımak için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fdc00-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="fdc00-105">Derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) kopyalama etkinliği ile veri taşıma için genel bir bakış sunar makalesi.</span><span class="sxs-lookup"><span data-stu-id="fdc00-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="fdc00-106">Desteklenen senaryolar</span><span class="sxs-lookup"><span data-stu-id="fdc00-106">Supported scenarios</span></span>
<span data-ttu-id="fdc00-107">Veri kopyalama **bir SQL Server veritabanından** aşağıdaki veri depolar:</span><span class="sxs-lookup"><span data-stu-id="fdc00-107">You can copy data **from a SQL Server database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="fdc00-108">Aşağıdaki veri depolarına verileri kopyalayabilirsiniz **bir SQL Server veritabanına**:</span><span class="sxs-lookup"><span data-stu-id="fdc00-108">You can copy data from the following data stores **to a SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="fdc00-109">Desteklenen SQL Server sürümleri</span><span class="sxs-lookup"><span data-stu-id="fdc00-109">Supported SQL Server versions</span></span>
<span data-ttu-id="fdc00-110">Veri kopyalama/barındırılan örneği şirket içi veya Azure SQL kimlik doğrulaması ve Windows kimlik doğrulaması kullanarak Iaas aşağıdaki sürümleri için bu SQL Server bağlayıcı desteği: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="fdc00-110">This SQL Server connector support copying data from/to the following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="fdc00-111">Bağlantıyı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="fdc00-111">Enabling connectivity</span></span>
<span data-ttu-id="fdc00-112">Kavramlar ve şirket içi barındırılan SQL Server ile veya (altyapı-bir hizmet olarak) Azure Iaas Vm'lerine bağlanmak için gerekli adımları aynıdır.</span><span class="sxs-lookup"><span data-stu-id="fdc00-112">The concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are the same.</span></span> <span data-ttu-id="fdc00-113">Her iki durumda da, veri yönetimi ağ geçidi bağlantısı için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-113">In both cases, you need to use Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="fdc00-114">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale veri yönetimi ağ geçidi ve ağ geçidi kurun ayarlama hakkında adım adım yönergeleri hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="fdc00-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="fdc00-115">Bir ağ geçidi örneği SQL Server ile bağlanmak için bir önkoşul ayardır.</span><span class="sxs-lookup"><span data-stu-id="fdc00-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="fdc00-116">Ağ geçidi aynı şirket içi makineye veya Bulut VM örneği üzerinde daha iyi performans için SQL sunucusu olarak yükleyebilirsiniz olsa da, bunları farklı makinelere yüklemeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-116">While you can install gateway on the same on-premises machine or cloud VM instance as the SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="fdc00-117">Ağ geçidi ve SQL Server ayrı makinelerde sahip kaynak çekişmesini azaltır.</span><span class="sxs-lookup"><span data-stu-id="fdc00-117">Having the gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="fdc00-118">Başlarken</span><span class="sxs-lookup"><span data-stu-id="fdc00-118">Getting started</span></span>
<span data-ttu-id="fdc00-119">Farklı araçlar/API'lerini kullanarak bir şirket içi SQL Server veritabanından/gelen verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fdc00-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="fdc00-120">Bir işlem hattı oluşturmak için en kolay yolu kullanmaktır **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="fdc00-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="fdc00-121">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) veri kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="fdc00-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="fdc00-122">Bir işlem hattı oluşturmak için aşağıdaki araçları kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu**, **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="fdc00-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="fdc00-123">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="fdc00-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="fdc00-124">Araçlar ya da API'leri kullanıp bir havuz veri deposu için bir kaynak veri deposundan verileri taşır bir ardışık düzen oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fdc00-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="fdc00-125">Oluşturma bir **veri fabrikası**.</span><span class="sxs-lookup"><span data-stu-id="fdc00-125">Create a **data factory**.</span></span> <span data-ttu-id="fdc00-126">Veri Fabrikası bir veya daha fazla ardışık düzen içerebilir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="fdc00-127">Oluşturma **bağlantılı Hizmetleri** girdi ve çıktı verilerini bağlamak için veri fabrikanıza depolar.</span><span class="sxs-lookup"><span data-stu-id="fdc00-127">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="fdc00-128">Örneğin, bir Azure blob depolama alanına bir SQL Server veritabanından veri kopyalıyorsanız, SQL Server veritabanı ve Azure depolama hesabı veri fabrikanıza bağlamak için iki bağlı hizmet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fdc00-128">For example, if you are copying data from a SQL Server database to an Azure blob storage, you create two linked services to link your SQL Server database and Azure storage account to your data factory.</span></span> <span data-ttu-id="fdc00-129">SQL Server veritabanına özel bağlantılı hizmet özellikleri için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="fdc00-129">For linked service properties that are specific to SQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="fdc00-130">Oluşturma **veri kümeleri** kopyalama işlemi için girdi ve çıktı verilerini temsil etmek için.</span><span class="sxs-lookup"><span data-stu-id="fdc00-130">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="fdc00-131">Son adımda bahsedilen örnekte giriş verilerini içeren, SQL Server veritabanında SQL tablosu belirtmek için bir veri kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fdc00-131">In the example mentioned in the last step, you create a dataset to specify the SQL table in your SQL Server database that contains the input data.</span></span> <span data-ttu-id="fdc00-132">Ve blob kapsayıcısında ve SQL Server veritabanından kopyalanan verileri tutan klasör belirtmek için başka bir veri kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fdc00-132">And, you create another dataset to specify the blob container and the folder that holds the data copied from the SQL Server database.</span></span> <span data-ttu-id="fdc00-133">SQL Server veritabanına özel veri kümesi özellikleri için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="fdc00-133">For dataset properties that are specific to SQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="fdc00-134">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="fdc00-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="fdc00-135">Daha önce bahsedilen örnekte SqlSource bir kaynak ve BlobSink havuzu olarak kopya etkinliği için kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="fdc00-135">In the example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="fdc00-136">SQL Server veritabanına Azure Blob depolama alanından kopyalıyorsanız benzer şekilde, BlobSource ve SqlSink kopyalama etkinliği kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="fdc00-136">Similarly, if you are copying from Azure Blob Storage to SQL Server Database, you use BlobSource and SqlSink in the copy activity.</span></span> <span data-ttu-id="fdc00-137">SQL Server veritabanına belirli kopyalama etkinliği özellikleri için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="fdc00-137">For copy activity properties that are specific to SQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="fdc00-138">Bir veri deposu bir kaynak veya bir havuz nasıl kullanılacağı hakkında daha fazla bilgi için önceki bölümde, veri deposu için bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fdc00-138">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="fdc00-139">Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fdc00-139">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="fdc00-140">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, JSON biçimini kullanarak bu Data Factory varlıklarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="fdc00-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="fdc00-141">/ Şirket içi SQL Server veritabanından veri kopyalamak için kullanılan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples-for-copying-data-from-and-to-sql-server) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="fdc00-141">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="fdc00-142">Aşağıdaki bölümler, SQL Server Data Factory varlıklarını belirli tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="fdc00-142">The following sections provide details about JSON properties that are used to define Data Factory entities specific to SQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="fdc00-143">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="fdc00-143">Linked service properties</span></span>
<span data-ttu-id="fdc00-144">Bağlı hizmet türü oluşturma **OnPremisesSqlServer** bir şirket içi SQL Server veritabanını data factory'ye bağlamak için.</span><span class="sxs-lookup"><span data-stu-id="fdc00-144">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="fdc00-145">Aşağıdaki tabloda şirket içi SQL Server bağlantılı hizmete özgü JSON öğeleri açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdc00-145">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="fdc00-146">Aşağıdaki tabloda, SQL Server bağlantılı hizmete özgü JSON öğeleri açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdc00-146">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="fdc00-147">Özellik</span><span class="sxs-lookup"><span data-stu-id="fdc00-147">Property</span></span> | <span data-ttu-id="fdc00-148">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdc00-148">Description</span></span> | <span data-ttu-id="fdc00-149">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fdc00-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fdc00-150">type</span><span class="sxs-lookup"><span data-stu-id="fdc00-150">type</span></span> |<span data-ttu-id="fdc00-151">Type özelliği ayarlanmalıdır: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="fdc00-151">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="fdc00-152">Evet</span><span class="sxs-lookup"><span data-stu-id="fdc00-152">Yes</span></span> |
| <span data-ttu-id="fdc00-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="fdc00-153">connectionString</span></span> |<span data-ttu-id="fdc00-154">SQL kimlik doğrulaması veya Windows kimlik doğrulaması kullanarak şirket içi SQL Server veritabanına bağlanmak için gereken connectionString bilgilerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="fdc00-154">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="fdc00-155">Evet</span><span class="sxs-lookup"><span data-stu-id="fdc00-155">Yes</span></span> |
| <span data-ttu-id="fdc00-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="fdc00-156">gatewayName</span></span> |<span data-ttu-id="fdc00-157">Data Factory hizmetinin şirket içi SQL Server veritabanına bağlanmak için kullanması gereken ağ geçidinin adı.</span><span class="sxs-lookup"><span data-stu-id="fdc00-157">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="fdc00-158">Evet</span><span class="sxs-lookup"><span data-stu-id="fdc00-158">Yes</span></span> |
| <span data-ttu-id="fdc00-159">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="fdc00-159">username</span></span> |<span data-ttu-id="fdc00-160">Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="fdc00-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="fdc00-161">Örnek: **domainname\\kullanıcıadı**.</span><span class="sxs-lookup"><span data-stu-id="fdc00-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="fdc00-162">Hayır</span><span class="sxs-lookup"><span data-stu-id="fdc00-162">No</span></span> |
| <span data-ttu-id="fdc00-163">password</span><span class="sxs-lookup"><span data-stu-id="fdc00-163">password</span></span> |<span data-ttu-id="fdc00-164">Kullanıcı adı için belirtilen kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="fdc00-164">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="fdc00-165">Hayır</span><span class="sxs-lookup"><span data-stu-id="fdc00-165">No</span></span> |

<span data-ttu-id="fdc00-166">Kimlik bilgilerini kullanarak şifreleyebilirsiniz **yeni AzureRmDataFactoryEncryptValue** cmdlet'i ve bunları aşağıdaki örnekte gösterildiği gibi bağlantı dizesini kullanın (**EncryptedCredential** özellik):</span><span class="sxs-lookup"><span data-stu-id="fdc00-166">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="fdc00-167">Örnekler</span><span class="sxs-lookup"><span data-stu-id="fdc00-167">Samples</span></span>
<span data-ttu-id="fdc00-168">**SQL kimlik doğrulaması kullanarak JSON**</span><span class="sxs-lookup"><span data-stu-id="fdc00-168">**JSON for using SQL Authentication**</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
<span data-ttu-id="fdc00-169">**Windows kimlik doğrulaması kullanmak için JSON**</span><span class="sxs-lookup"><span data-stu-id="fdc00-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="fdc00-170">Veri Yönetimi ağ geçidi, şirket içi SQL Server veritabanına bağlanmak için belirtilen kullanıcı hesabının kimliğine bürün.</span><span class="sxs-lookup"><span data-stu-id="fdc00-170">Data Management Gateway will impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="fdc00-171">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="fdc00-171">Dataset properties</span></span>
<span data-ttu-id="fdc00-172">Bir veri türünde kullanılan örneklerinde **SqlServerTable** bir SQL Server veritabanındaki bir tablo temsil etmek için.</span><span class="sxs-lookup"><span data-stu-id="fdc00-172">In the samples, you have used a dataset of type **SqlServerTable** to represent a table in a SQL Server database.</span></span>  

<span data-ttu-id="fdc00-173">Bölümler & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="fdc00-173">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="fdc00-174">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (SQL Server, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="fdc00-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="fdc00-175">TypeProperties bölümü dataset her tür için farklıdır ve verilerin veri deposunda konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdc00-175">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="fdc00-176">**TypeProperties** veri kümesi için bir bölüm türü **SqlServerTable** aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="fdc00-176">The **typeProperties** section for the dataset of type **SqlServerTable** has the following properties:</span></span>

| <span data-ttu-id="fdc00-177">Özellik</span><span class="sxs-lookup"><span data-stu-id="fdc00-177">Property</span></span> | <span data-ttu-id="fdc00-178">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdc00-178">Description</span></span> | <span data-ttu-id="fdc00-179">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fdc00-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fdc00-180">tableName</span><span class="sxs-lookup"><span data-stu-id="fdc00-180">tableName</span></span> |<span data-ttu-id="fdc00-181">Tablo veya Görünüm hizmeti bağlı SQL Server veritabanı örneğinde başvurduğu adı.</span><span class="sxs-lookup"><span data-stu-id="fdc00-181">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="fdc00-182">Evet</span><span class="sxs-lookup"><span data-stu-id="fdc00-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="fdc00-183">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="fdc00-183">Copy activity properties</span></span>
<span data-ttu-id="fdc00-184">Bir SQL Server veritabanından veri taşıyorsanız, kaynak türü için kopyalama etkinliğinde ayarladığınız **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="fdc00-184">If you are moving data from a SQL Server database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="fdc00-185">Bir SQL Server veritabanına veri taşıyorsanız, benzer şekilde, Havuz türü için kopyalama etkinliğinde ayarladığınız **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="fdc00-185">Similarly, if you are moving data to a SQL Server database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="fdc00-186">Bu bölümde SqlSource ve SqlSink tarafından desteklenen özellikler listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdc00-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="fdc00-187">Bölümler & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz: [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="fdc00-187">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="fdc00-188">Ad, açıklama, giriş ve çıkış tabloları ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="fdc00-189">Kopyalama etkinliği yalnızca bir girdi alır ve tek bir çıktı üretir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-189">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="fdc00-190">Oysa etkinliğin typeProperties bölümündeki özellikler her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-190">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="fdc00-191">Kopya etkinliği için bunlar türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-191">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="fdc00-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="fdc00-192">SqlSource</span></span>
<span data-ttu-id="fdc00-193">Kopyalama etkinliği kaynağında türü olduğunda **SqlSource**, aşağıdaki özellikler mevcuttur **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="fdc00-193">When source in a copy activity is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="fdc00-194">Özellik</span><span class="sxs-lookup"><span data-stu-id="fdc00-194">Property</span></span> | <span data-ttu-id="fdc00-195">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdc00-195">Description</span></span> | <span data-ttu-id="fdc00-196">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="fdc00-196">Allowed values</span></span> | <span data-ttu-id="fdc00-197">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fdc00-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fdc00-198">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="fdc00-198">sqlReaderQuery</span></span> |<span data-ttu-id="fdc00-199">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="fdc00-199">Use the custom query to read data.</span></span> |<span data-ttu-id="fdc00-200">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="fdc00-200">SQL query string.</span></span> <span data-ttu-id="fdc00-201">Örneğin: seçin * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="fdc00-201">For example: select * from MyTable.</span></span> <span data-ttu-id="fdc00-202">Birden çok tablo girdi veri kümesi tarafından başvurulan veritabanından başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-202">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="fdc00-203">Belirtilmezse, yürütülen SQL deyimi: MyTable arasından seçin.</span><span class="sxs-lookup"><span data-stu-id="fdc00-203">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="fdc00-204">Hayır</span><span class="sxs-lookup"><span data-stu-id="fdc00-204">No</span></span> |
| <span data-ttu-id="fdc00-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="fdc00-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="fdc00-206">Kaynak tablodan veri okuyan saklı yordamın adı.</span><span class="sxs-lookup"><span data-stu-id="fdc00-206">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="fdc00-207">Saklı yordam adı.</span><span class="sxs-lookup"><span data-stu-id="fdc00-207">Name of the stored procedure.</span></span> <span data-ttu-id="fdc00-208">Son SQL deyimi SELECT deyimi içinde saklı yordamı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-208">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="fdc00-209">Hayır</span><span class="sxs-lookup"><span data-stu-id="fdc00-209">No</span></span> |
| <span data-ttu-id="fdc00-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="fdc00-210">storedProcedureParameters</span></span> |<span data-ttu-id="fdc00-211">Saklı yordam parametreleri.</span><span class="sxs-lookup"><span data-stu-id="fdc00-211">Parameters for the stored procedure.</span></span> |<span data-ttu-id="fdc00-212">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="fdc00-212">Name/value pairs.</span></span> <span data-ttu-id="fdc00-213">Adları ve büyük/küçük harf parametrelerinin adlarını ve saklı yordam parametreleri büyük/küçük harf eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-213">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="fdc00-214">Hayır</span><span class="sxs-lookup"><span data-stu-id="fdc00-214">No</span></span> |

<span data-ttu-id="fdc00-215">Varsa **sqlReaderQuery** belirtilen SqlSource için kopyalama etkinliği veri almak için SQL Server veritabanı kaynağında bu sorguyu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="fdc00-215">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="fdc00-216">Alternatif olarak, bir saklı yordam belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (saklı yordam parametreleri alıyorsa).</span><span class="sxs-lookup"><span data-stu-id="fdc00-216">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="fdc00-217">SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz yapısı bölümünde tanımlanan sütunları SQL Server veritabanına karşı çalıştırmak için seçme sorgusu oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fdc00-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="fdc00-218">Veri kümesi tanımı yapısına sahip değilse, tüm sütunları tablodan seçilir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-218">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="fdc00-219">Kullandığınızda **sqlReaderStoredProcedureName**, yine de için bir değer belirtmeniz gerekiyorsa **tableName** JSON veri kümesi bir özellik.</span><span class="sxs-lookup"><span data-stu-id="fdc00-219">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="fdc00-220">Yine de bu tabloya karşı gerçekleştirilen başka doğrulama vardır.</span><span class="sxs-lookup"><span data-stu-id="fdc00-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="fdc00-221">SqlSink</span><span class="sxs-lookup"><span data-stu-id="fdc00-221">SqlSink</span></span>
<span data-ttu-id="fdc00-222">**SqlSink** aşağıdaki özellikleri destekler:</span><span class="sxs-lookup"><span data-stu-id="fdc00-222">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="fdc00-223">Özellik</span><span class="sxs-lookup"><span data-stu-id="fdc00-223">Property</span></span> | <span data-ttu-id="fdc00-224">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdc00-224">Description</span></span> | <span data-ttu-id="fdc00-225">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="fdc00-225">Allowed values</span></span> | <span data-ttu-id="fdc00-226">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fdc00-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fdc00-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="fdc00-227">writeBatchTimeout</span></span> |<span data-ttu-id="fdc00-228">Toplu ekleme işlemi zaman aşımına uğramadan önce tamamlamak bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="fdc00-228">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="fdc00-229">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="fdc00-229">timespan</span></span><br/><br/> <span data-ttu-id="fdc00-230">Örnek: "00: 30:00" (30 dakika).</span><span class="sxs-lookup"><span data-stu-id="fdc00-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="fdc00-231">Hayır</span><span class="sxs-lookup"><span data-stu-id="fdc00-231">No</span></span> |
| <span data-ttu-id="fdc00-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="fdc00-232">writeBatchSize</span></span> |<span data-ttu-id="fdc00-233">Arabellek boyutu writeBatchSize ulaştığında veri SQL tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="fdc00-233">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="fdc00-234">Tamsayı (satır sayısı)</span><span class="sxs-lookup"><span data-stu-id="fdc00-234">Integer (number of rows)</span></span> |<span data-ttu-id="fdc00-235">Hayır (varsayılan: 10000)</span><span class="sxs-lookup"><span data-stu-id="fdc00-235">No (default: 10000)</span></span> |
| <span data-ttu-id="fdc00-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="fdc00-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="fdc00-237">Belirli bir dilimle verilerinin temizlenmesini şekilde yürütmek kopyalama etkinliği sorgusunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="fdc00-237">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="fdc00-238">Daha fazla bilgi için bkz: [yinelenebilir kopyalama](#repeatable-copy) bölümü.</span><span class="sxs-lookup"><span data-stu-id="fdc00-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="fdc00-239">Sorgu bildirimi.</span><span class="sxs-lookup"><span data-stu-id="fdc00-239">A query statement.</span></span> |<span data-ttu-id="fdc00-240">Hayır</span><span class="sxs-lookup"><span data-stu-id="fdc00-240">No</span></span> |
| <span data-ttu-id="fdc00-241">Sliceıdentifiercolumnname</span><span class="sxs-lookup"><span data-stu-id="fdc00-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="fdc00-242">Kopyalama etkinliği'nin ne zaman yeniden çalıştırılacağını belirli bir dilim verileri temizlemek için kullanılan otomatik dilim tanımlayıcı doldurmak için sütun adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="fdc00-242">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="fdc00-243">Daha fazla bilgi için bkz: [yinelenebilir kopyalama](#repeatable-copy) bölümü.</span><span class="sxs-lookup"><span data-stu-id="fdc00-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="fdc00-244">Binary(32) veri türüne sahip bir sütunun sütun adı.</span><span class="sxs-lookup"><span data-stu-id="fdc00-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="fdc00-245">Hayır</span><span class="sxs-lookup"><span data-stu-id="fdc00-245">No</span></span> |
| <span data-ttu-id="fdc00-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="fdc00-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="fdc00-247">Saklı yordam adı hedef tabloda bu upserts (güncelleştirmeler/ekler) verileri.</span><span class="sxs-lookup"><span data-stu-id="fdc00-247">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="fdc00-248">Saklı yordam adı.</span><span class="sxs-lookup"><span data-stu-id="fdc00-248">Name of the stored procedure.</span></span> |<span data-ttu-id="fdc00-249">Hayır</span><span class="sxs-lookup"><span data-stu-id="fdc00-249">No</span></span> |
| <span data-ttu-id="fdc00-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="fdc00-250">storedProcedureParameters</span></span> |<span data-ttu-id="fdc00-251">Saklı yordam parametreleri.</span><span class="sxs-lookup"><span data-stu-id="fdc00-251">Parameters for the stored procedure.</span></span> |<span data-ttu-id="fdc00-252">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="fdc00-252">Name/value pairs.</span></span> <span data-ttu-id="fdc00-253">Adları ve büyük/küçük harf parametrelerinin adlarını ve saklı yordam parametreleri büyük/küçük harf eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-253">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="fdc00-254">Hayır</span><span class="sxs-lookup"><span data-stu-id="fdc00-254">No</span></span> |
| <span data-ttu-id="fdc00-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="fdc00-255">sqlWriterTableType</span></span> |<span data-ttu-id="fdc00-256">Saklı yordam, kullanılacak tablo türü adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="fdc00-256">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="fdc00-257">Kopyalama etkinliği taşınan veri geçici bir tablo bu tablo türü ile kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-257">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="fdc00-258">Saklı yordam kodu ardından var olan verilerle kopyalanan verileri birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdc00-258">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="fdc00-259">Bir tablo türü adı.</span><span class="sxs-lookup"><span data-stu-id="fdc00-259">A table type name.</span></span> |<span data-ttu-id="fdc00-260">Hayır</span><span class="sxs-lookup"><span data-stu-id="fdc00-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-to-sql-server"></a><span data-ttu-id="fdc00-261">Gelen ve SQL Server veri kopyalamak için JSON örnekleri</span><span class="sxs-lookup"><span data-stu-id="fdc00-261">JSON examples for copying data from and to SQL Server</span></span>
<span data-ttu-id="fdc00-262">Aşağıdaki örnekleri kullanarak bir işlem hattı oluşturmak için kullanabileceğiniz örnek JSON tanımları sağlar [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fdc00-262">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="fdc00-263">Aşağıdaki örnekler ve SQL Server ve Azure Blob Storage veri kopyalamak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-263">The following samples show how to copy data to and from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="fdc00-264">Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden herhangi birine belirtildiği havuzlarını kaynakları [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kopya etkinliği Azure Data Factory kullanarak.</span><span class="sxs-lookup"><span data-stu-id="fdc00-264">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-to-azure-blob"></a><span data-ttu-id="fdc00-265">Örnek: veri SQL Server'dan Azure Blob kopyalama</span><span class="sxs-lookup"><span data-stu-id="fdc00-265">Example: Copy data from SQL Server to Azure Blob</span></span>
<span data-ttu-id="fdc00-266">Aşağıdaki örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="fdc00-266">The following sample shows:</span></span>

1. <span data-ttu-id="fdc00-267">Bağlı hizmet türü [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fdc00-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="fdc00-268">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fdc00-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="fdc00-269">Bir giriş [dataset](data-factory-create-datasets.md) türü [SqlServerTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fdc00-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="fdc00-270">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fdc00-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="fdc00-271">[Ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [SqlSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="fdc00-271">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="fdc00-272">Örnek time series verilerini bir SQL Server tablosundan saatte bir Azure blob kopyalar.</span><span class="sxs-lookup"><span data-stu-id="fdc00-272">The sample copies time-series data from a SQL Server table to an Azure blob every hour.</span></span> <span data-ttu-id="fdc00-273">Bu örnekler kullanılan JSON özellikleri örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="fdc00-273">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="fdc00-274">İlk adım olarak, veri yönetimi ağ geçidi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="fdc00-274">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="fdc00-275">Yönergeler bulunan [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="fdc00-275">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="fdc00-276">**SQL Server bağlantılı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="fdc00-276">**SQL Server linked service**</span></span>
```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="fdc00-277">**Azure Blob storage bağlı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="fdc00-277">**Azure Blob storage linked service**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="fdc00-278">**SQL Server girdi veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="fdc00-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="fdc00-279">Örnek SQL Server'da bir tablo "MyTable" oluşturulur ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="fdc00-279">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="fdc00-280">Tek bir veri kümesini kullanarak aynı veritabanı içinde birden çok tablo üzerinde sorgulayabilir, ancak tek bir tablo için veri kümesi'nin tableName typeProperty kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fdc00-280">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="fdc00-281">"Dış" ayarı: "true" bildirir Data Factory hizmetinin veri kümesi data factory dış ve veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="fdc00-281">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
  "name": "SqlServerInput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
<span data-ttu-id="fdc00-282">**Azure Blob dataset çıktı**</span><span class="sxs-lookup"><span data-stu-id="fdc00-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="fdc00-283">Veri her saat yeni bir bloba yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="fdc00-283">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="fdc00-284">Blob klasör yolu dinamik işlenmekte olan dilim başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-284">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="fdc00-285">Klasör yolu yıl, ay, gün ve saat bölümleri başlangıç saatini kullanır.</span><span class="sxs-lookup"><span data-stu-id="fdc00-285">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="fdc00-286">**Kopyalama etkinliği ile kanalı**</span><span class="sxs-lookup"><span data-stu-id="fdc00-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="fdc00-287">Ardışık Düzen bu girdi ve çıktı veri kümeleri kullanmak üzere yapılandırıldığı ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-287">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="fdc00-288">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **SqlSource** ve **havuz** türü ayarlanmış **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="fdc00-288">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="fdc00-289">SQL sorgusu için belirtilen **SqlReaderQuery** özelliği veri kopyalamak için son bir saat içindeki seçer.</span><span class="sxs-lookup"><span data-stu-id="fdc00-289">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```
<span data-ttu-id="fdc00-290">Bu örnekte, **sqlReaderQuery** SqlSource için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-290">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="fdc00-291">Kopyalama etkinliği bu sorguyu veri almak için SQL Server veritabanı kaynağına karşı çalışır.</span><span class="sxs-lookup"><span data-stu-id="fdc00-291">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="fdc00-292">Alternatif olarak, bir saklı yordam belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (saklı yordam parametreleri alıyorsa).</span><span class="sxs-lookup"><span data-stu-id="fdc00-292">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="fdc00-293">SqlReaderQuery girdi veri kümesi tarafından başvurulan veritabanına birden çok tablolarına başvuruda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-293">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="fdc00-294">Yalnızca veri kümesi'nin tableName typeProperty ayarlamak tabloya sınırlı değildir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-294">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="fdc00-295">SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz yapısı bölümünde tanımlanan sütunları SQL Server veritabanına karşı çalıştırmak için seçme sorgusu oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fdc00-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="fdc00-296">Veri kümesi tanımı yapısına sahip değilse, tüm sütunları tablodan seçilir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-296">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="fdc00-297">Bkz: [Sql kaynağı](#sqlsource) bölüm ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) SqlSource ve BlobSink tarafından desteklenen özelliklerin listesi için.</span><span class="sxs-lookup"><span data-stu-id="fdc00-297">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-to-sql-server"></a><span data-ttu-id="fdc00-298">Örnek: verileri Azure Blob'tan SQL sunucusuna kopyalayın</span><span class="sxs-lookup"><span data-stu-id="fdc00-298">Example: Copy data from Azure Blob to SQL Server</span></span>
<span data-ttu-id="fdc00-299">Aşağıdaki örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="fdc00-299">The following sample shows:</span></span>

1. <span data-ttu-id="fdc00-300">Türündeki bağlı hizmetin [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fdc00-300">The linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="fdc00-301">Türündeki bağlı hizmetin [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fdc00-301">The linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="fdc00-302">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fdc00-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="fdc00-303">Bir çıkış [dataset](data-factory-create-datasets.md) türü [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fdc00-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="fdc00-304">[Ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) ve [SqlSink](#sql-server-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="fdc00-304">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="fdc00-305">Zaman serisi bir SQL Server verileri Azure blob örnek kopyaları saatte tablo.</span><span class="sxs-lookup"><span data-stu-id="fdc00-305">The sample copies time-series data from an Azure blob to a SQL Server table every hour.</span></span> <span data-ttu-id="fdc00-306">Bu örnekler kullanılan JSON özellikleri örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="fdc00-306">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="fdc00-307">**SQL Server bağlantılı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="fdc00-307">**SQL Server linked service**</span></span>

```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="fdc00-308">**Azure Blob storage bağlı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="fdc00-308">**Azure Blob storage linked service**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="fdc00-309">**Azure Blob girdi veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="fdc00-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="fdc00-310">Veri toplanma yeni blob üzerinden saatte (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="fdc00-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="fdc00-311">Blob klasör yolu ve dosya adı dinamik olarak değerlendirilir işleniyor dilim başlangıç zamanı temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="fdc00-311">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="fdc00-312">Klasör yolu yıl, ay ve gün kısmını başlangıç saati ve dosya adı başlangıç zamanı saat bölümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="fdc00-312">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="fdc00-313">"dış": "true" ayarı, veri kümesi data factory dış ve veri fabrikasında bir etkinlik tarafından üretilen değil Data Factory hizmetinin bildirir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-313">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
<span data-ttu-id="fdc00-314">**SQL Server çıktı veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="fdc00-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="fdc00-315">Örnek verileri SQL Server'da "MyTable" adlı bir tablo kopyalar.</span><span class="sxs-lookup"><span data-stu-id="fdc00-315">The sample copies data to a table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="fdc00-316">Blob CSV dosyasında içerecek şekilde beklediğiniz gibi tablo SQL Server ile aynı sayıda sütun oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fdc00-316">Create the table in SQL Server with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="fdc00-317">Yeni satırlar tabloya saatte eklenir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-317">New rows are added to the table every hour.</span></span>

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="fdc00-318">**Kopyalama etkinliği ile kanalı**</span><span class="sxs-lookup"><span data-stu-id="fdc00-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="fdc00-319">Ardışık Düzen bu girdi ve çıktı veri kümeleri kullanmak üzere yapılandırıldığı ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-319">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="fdc00-320">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **BlobSource** ve **havuz** türü ayarlanmış **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="fdc00-320">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": " SqlServerOutput "
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="fdc00-321">Bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="fdc00-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="fdc00-322">Uzak bağlantıları kabul etmek için SQL Server'ınızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fdc00-322">Configure your SQL Server to accept remote connections.</span></span> <span data-ttu-id="fdc00-323">Başlatma **SQL Server Management Studio**, sağ **server**, tıklatıp **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="fdc00-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="fdc00-324">Seçin **bağlantıları** listesi ve onay **sunucusuna uzaktan bağlantılara izin**.</span><span class="sxs-lookup"><span data-stu-id="fdc00-324">Select **Connections** from the list and check **Allow remote connections to the server**.</span></span>

    ![Uzak bağlantıları etkinleştir](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="fdc00-326">Bkz: [uzaktan erişim sunucu yapılandırma seçeneğini yapılandırma](https://msdn.microsoft.com/library/ms191464.aspx) ayrıntılı adımlar için.</span><span class="sxs-lookup"><span data-stu-id="fdc00-326">See [Configure the remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="fdc00-327">Başlatma **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="fdc00-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="fdc00-328">Genişletme **SQL Server Ağ Yapılandırması** ve seçin, örneğin **MSSQLSERVER protokolleri**.</span><span class="sxs-lookup"><span data-stu-id="fdc00-328">Expand **SQL Server Network Configuration** for the instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="fdc00-329">Sağ bölmede protokolleri görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-329">You should see protocols in the right-pane.</span></span> <span data-ttu-id="fdc00-330">Sağ tıklayarak TCP/IP'yi etkinleştirin **TCP/IP'yi** tıklatıp **etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="fdc00-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![TCP/IP'yi etkinleştirin](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="fdc00-332">Bkz: [etkinleştirmek veya devre dışı bir sunucu ağ protokolü](https://msdn.microsoft.com/library/ms191294.aspx) ayrıntı ve TCP/IP protokolünün etkinleştirilmesi alternatif yolu.</span><span class="sxs-lookup"><span data-stu-id="fdc00-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="fdc00-333">Aynı pencerede çift **TCP/IP'yi** başlatmak için **TCP/IP özelliklerini** penceresi.</span><span class="sxs-lookup"><span data-stu-id="fdc00-333">In the same window, double-click **TCP/IP** to launch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="fdc00-334">Geçiş **IP adreslerini** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="fdc00-334">Switch to the **IP Addresses** tab.</span></span> <span data-ttu-id="fdc00-335">Kaydırma görmek için **IPAll** bölümü.</span><span class="sxs-lookup"><span data-stu-id="fdc00-335">Scroll down to see **IPAll** section.</span></span> <span data-ttu-id="fdc00-336">Aşağı Not ** TCP bağlantı noktası ** (varsayılan değer **1433**).</span><span class="sxs-lookup"><span data-stu-id="fdc00-336">Note down the **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="fdc00-337">Oluşturma bir **Windows Güvenlik Duvarı Kuralı** Bu bağlantı noktası üzerinden gelen trafiğe izin vermek için makinede.</span><span class="sxs-lookup"><span data-stu-id="fdc00-337">Create a **rule for the Windows Firewall** on the machine to allow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="fdc00-338">**Bağlantıyı doğrulama**: tam olarak nitelenmiş adını kullanarak SQL Server'a bağlanmak için farklı bir makineden SQL Server Management Studio kullanın.</span><span class="sxs-lookup"><span data-stu-id="fdc00-338">**Verify connection**: To connect to the SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="fdc00-339">Örneğin: "<machine>.<domain>. Corp.<company>.com, 1433. "</span><span class="sxs-lookup"><span data-stu-id="fdc00-339">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="fdc00-340">Bkz: [şirket içi kaynakları ve veri yönetimi ağ geçidi ile bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="fdc00-340">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="fdc00-341">Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="fdc00-341">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="fdc00-342">Hedef veritabanında kimlik sütunu</span><span class="sxs-lookup"><span data-stu-id="fdc00-342">Identity columns in the target database</span></span>
<span data-ttu-id="fdc00-343">Bu bölümde kimlik sütunu içeren bir kaynak tablo verileri bir kimlik sütunu hedef tabloyla kopyalayan bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdc00-343">This section provides an example that copies data from a source table with no identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="fdc00-344">**Kaynak tablosu:**</span><span class="sxs-lookup"><span data-stu-id="fdc00-344">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="fdc00-345">**Hedef Tablo:**</span><span class="sxs-lookup"><span data-stu-id="fdc00-345">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="fdc00-346">Hedef tabloda bir kimlik sütunu olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="fdc00-346">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="fdc00-347">**Kaynak veri kümesi JSON tanımı**</span><span class="sxs-lookup"><span data-stu-id="fdc00-347">**Source dataset JSON definition**</span></span>

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="fdc00-348">**Hedef veri kümesi JSON tanımı**</span><span class="sxs-lookup"><span data-stu-id="fdc00-348">**Destination dataset JSON definition**</span></span>

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

<span data-ttu-id="fdc00-349">Kaynak ve hedef tablosu farklı şema sahip dikkat edin (hedef kimliğine sahip başka bir sütuna sahip).</span><span class="sxs-lookup"><span data-stu-id="fdc00-349">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="fdc00-350">Bu senaryoda, belirtmeniz gerekir. **yapısı** kimlik sütunu içermeyen hedef veri kümesi tanımında özelliği.</span><span class="sxs-lookup"><span data-stu-id="fdc00-350">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="fdc00-351">SQL havuz depolanan yordamı çağırma</span><span class="sxs-lookup"><span data-stu-id="fdc00-351">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="fdc00-352">Bkz: [kopyalama etkinliği SQL havuz için saklı yordam çağırma](data-factory-invoke-stored-procedure-from-copy-activity.md) makale SQL havuz ardışık kopyalama etkinliğinde bir saklı yordam çağırma örneği.</span><span class="sxs-lookup"><span data-stu-id="fdc00-352">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="fdc00-353">Tür eşlemesi için SQL server</span><span class="sxs-lookup"><span data-stu-id="fdc00-353">Type mapping for SQL server</span></span>
<span data-ttu-id="fdc00-354">Bölümünde belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopya etkinliği aşağıdaki 2 adımlı yaklaşımı türleriyle havuz için kaynak türünden otomatik tür dönüşümleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="fdc00-354">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="fdc00-355">Yerel kaynak türlerinden .NET türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="fdc00-355">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="fdc00-356">.NET türünden yerel havuz türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="fdc00-356">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="fdc00-357">& SQL Server'dan veri taşıma olduğunda, aşağıdaki eşlemelerini SQL türü .NET türü ve tersi yönde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fdc00-357">When moving data to & from SQL server, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="fdc00-358">ADO.NET için SQL Server veri türü eşlemesi aynı eşlemedir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-358">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="fdc00-359">SQL Server veritabanı altyapısı türü</span><span class="sxs-lookup"><span data-stu-id="fdc00-359">SQL Server Database Engine type</span></span> | <span data-ttu-id="fdc00-360">.NET framework türü</span><span class="sxs-lookup"><span data-stu-id="fdc00-360">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="fdc00-361">bigint</span><span class="sxs-lookup"><span data-stu-id="fdc00-361">bigint</span></span> |<span data-ttu-id="fdc00-362">Int64</span><span class="sxs-lookup"><span data-stu-id="fdc00-362">Int64</span></span> |
| <span data-ttu-id="fdc00-363">İkili</span><span class="sxs-lookup"><span data-stu-id="fdc00-363">binary</span></span> |<span data-ttu-id="fdc00-364">Byte]</span><span class="sxs-lookup"><span data-stu-id="fdc00-364">Byte[]</span></span> |
| <span data-ttu-id="fdc00-365">bit</span><span class="sxs-lookup"><span data-stu-id="fdc00-365">bit</span></span> |<span data-ttu-id="fdc00-366">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="fdc00-366">Boolean</span></span> |
| <span data-ttu-id="fdc00-367">char</span><span class="sxs-lookup"><span data-stu-id="fdc00-367">char</span></span> |<span data-ttu-id="fdc00-368">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="fdc00-368">String, Char[]</span></span> |
| <span data-ttu-id="fdc00-369">Tarih</span><span class="sxs-lookup"><span data-stu-id="fdc00-369">date</span></span> |<span data-ttu-id="fdc00-370">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="fdc00-370">DateTime</span></span> |
| <span data-ttu-id="fdc00-371">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="fdc00-371">Datetime</span></span> |<span data-ttu-id="fdc00-372">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="fdc00-372">DateTime</span></span> |
| <span data-ttu-id="fdc00-373">datetime2</span><span class="sxs-lookup"><span data-stu-id="fdc00-373">datetime2</span></span> |<span data-ttu-id="fdc00-374">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="fdc00-374">DateTime</span></span> |
| <span data-ttu-id="fdc00-375">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="fdc00-375">Datetimeoffset</span></span> |<span data-ttu-id="fdc00-376">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="fdc00-376">DateTimeOffset</span></span> |
| <span data-ttu-id="fdc00-377">Ondalık</span><span class="sxs-lookup"><span data-stu-id="fdc00-377">Decimal</span></span> |<span data-ttu-id="fdc00-378">Ondalık</span><span class="sxs-lookup"><span data-stu-id="fdc00-378">Decimal</span></span> |
| <span data-ttu-id="fdc00-379">FILESTREAM özniteliği (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="fdc00-379">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="fdc00-380">Byte]</span><span class="sxs-lookup"><span data-stu-id="fdc00-380">Byte[]</span></span> |
| <span data-ttu-id="fdc00-381">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="fdc00-381">Float</span></span> |<span data-ttu-id="fdc00-382">Çift</span><span class="sxs-lookup"><span data-stu-id="fdc00-382">Double</span></span> |
| <span data-ttu-id="fdc00-383">Görüntü</span><span class="sxs-lookup"><span data-stu-id="fdc00-383">image</span></span> |<span data-ttu-id="fdc00-384">Byte]</span><span class="sxs-lookup"><span data-stu-id="fdc00-384">Byte[]</span></span> |
| <span data-ttu-id="fdc00-385">Int</span><span class="sxs-lookup"><span data-stu-id="fdc00-385">int</span></span> |<span data-ttu-id="fdc00-386">Int32</span><span class="sxs-lookup"><span data-stu-id="fdc00-386">Int32</span></span> |
| <span data-ttu-id="fdc00-387">para</span><span class="sxs-lookup"><span data-stu-id="fdc00-387">money</span></span> |<span data-ttu-id="fdc00-388">Ondalık</span><span class="sxs-lookup"><span data-stu-id="fdc00-388">Decimal</span></span> |
| <span data-ttu-id="fdc00-389">nchar</span><span class="sxs-lookup"><span data-stu-id="fdc00-389">nchar</span></span> |<span data-ttu-id="fdc00-390">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="fdc00-390">String, Char[]</span></span> |
| <span data-ttu-id="fdc00-391">ntext</span><span class="sxs-lookup"><span data-stu-id="fdc00-391">ntext</span></span> |<span data-ttu-id="fdc00-392">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="fdc00-392">String, Char[]</span></span> |
| <span data-ttu-id="fdc00-393">sayısal</span><span class="sxs-lookup"><span data-stu-id="fdc00-393">numeric</span></span> |<span data-ttu-id="fdc00-394">Ondalık</span><span class="sxs-lookup"><span data-stu-id="fdc00-394">Decimal</span></span> |
| <span data-ttu-id="fdc00-395">nvarchar</span><span class="sxs-lookup"><span data-stu-id="fdc00-395">nvarchar</span></span> |<span data-ttu-id="fdc00-396">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="fdc00-396">String, Char[]</span></span> |
| <span data-ttu-id="fdc00-397">Gerçek</span><span class="sxs-lookup"><span data-stu-id="fdc00-397">real</span></span> |<span data-ttu-id="fdc00-398">Tek</span><span class="sxs-lookup"><span data-stu-id="fdc00-398">Single</span></span> |
| <span data-ttu-id="fdc00-399">rowVersion</span><span class="sxs-lookup"><span data-stu-id="fdc00-399">rowversion</span></span> |<span data-ttu-id="fdc00-400">Byte]</span><span class="sxs-lookup"><span data-stu-id="fdc00-400">Byte[]</span></span> |
| <span data-ttu-id="fdc00-401">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="fdc00-401">smalldatetime</span></span> |<span data-ttu-id="fdc00-402">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="fdc00-402">DateTime</span></span> |
| <span data-ttu-id="fdc00-403">tamsayı</span><span class="sxs-lookup"><span data-stu-id="fdc00-403">smallint</span></span> |<span data-ttu-id="fdc00-404">Int16</span><span class="sxs-lookup"><span data-stu-id="fdc00-404">Int16</span></span> |
| <span data-ttu-id="fdc00-405">küçük para</span><span class="sxs-lookup"><span data-stu-id="fdc00-405">smallmoney</span></span> |<span data-ttu-id="fdc00-406">Ondalık</span><span class="sxs-lookup"><span data-stu-id="fdc00-406">Decimal</span></span> |
| <span data-ttu-id="fdc00-407">sql_variant</span><span class="sxs-lookup"><span data-stu-id="fdc00-407">sql_variant</span></span> |<span data-ttu-id="fdc00-408">Nesne *</span><span class="sxs-lookup"><span data-stu-id="fdc00-408">Object *</span></span> |
| <span data-ttu-id="fdc00-409">Metin</span><span class="sxs-lookup"><span data-stu-id="fdc00-409">text</span></span> |<span data-ttu-id="fdc00-410">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="fdc00-410">String, Char[]</span></span> |
| <span data-ttu-id="fdc00-411">time</span><span class="sxs-lookup"><span data-stu-id="fdc00-411">time</span></span> |<span data-ttu-id="fdc00-412">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="fdc00-412">TimeSpan</span></span> |
| <span data-ttu-id="fdc00-413">timestamp</span><span class="sxs-lookup"><span data-stu-id="fdc00-413">timestamp</span></span> |<span data-ttu-id="fdc00-414">Byte]</span><span class="sxs-lookup"><span data-stu-id="fdc00-414">Byte[]</span></span> |
| <span data-ttu-id="fdc00-415">Mini tamsayı</span><span class="sxs-lookup"><span data-stu-id="fdc00-415">tinyint</span></span> |<span data-ttu-id="fdc00-416">Bayt</span><span class="sxs-lookup"><span data-stu-id="fdc00-416">Byte</span></span> |
| <span data-ttu-id="fdc00-417">benzersiz tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="fdc00-417">uniqueidentifier</span></span> |<span data-ttu-id="fdc00-418">GUID</span><span class="sxs-lookup"><span data-stu-id="fdc00-418">Guid</span></span> |
| <span data-ttu-id="fdc00-419">varbinary</span><span class="sxs-lookup"><span data-stu-id="fdc00-419">varbinary</span></span> |<span data-ttu-id="fdc00-420">Byte]</span><span class="sxs-lookup"><span data-stu-id="fdc00-420">Byte[]</span></span> |
| <span data-ttu-id="fdc00-421">varchar</span><span class="sxs-lookup"><span data-stu-id="fdc00-421">varchar</span></span> |<span data-ttu-id="fdc00-422">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="fdc00-422">String, Char[]</span></span> |
| <span data-ttu-id="fdc00-423">xml</span><span class="sxs-lookup"><span data-stu-id="fdc00-423">xml</span></span> |<span data-ttu-id="fdc00-424">XML</span><span class="sxs-lookup"><span data-stu-id="fdc00-424">Xml</span></span> |

## <a name="mapping-source-to-sink-columns"></a><span data-ttu-id="fdc00-425">Sütunları havuz için eşleme kaynağı</span><span class="sxs-lookup"><span data-stu-id="fdc00-425">Mapping source to sink columns</span></span>
<span data-ttu-id="fdc00-426">Kaynak veri kümesi sütunlarından havuz kümesinden sütunlara eşlemek için bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="fdc00-426">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="fdc00-427">Yinelenebilir kopyalama</span><span class="sxs-lookup"><span data-stu-id="fdc00-427">Repeatable copy</span></span>
<span data-ttu-id="fdc00-428">SQL Server veritabanına veri kopyalama, kopyalama etkinliği verileri varsayılan olarak havuz tabloya ekler.</span><span class="sxs-lookup"><span data-stu-id="fdc00-428">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="fdc00-429">Bunun yerine bir UPSERT gerçekleştirmek için bkz: [Repeatable yazmak için SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) makalesi.</span><span class="sxs-lookup"><span data-stu-id="fdc00-429">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="fdc00-430">İlişkisel veri kopyalama verileri depoladığında, Yinelenebilirlik istenmeyen sonuçları önlemek için göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="fdc00-430">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="fdc00-431">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdc00-431">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="fdc00-432">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdc00-432">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="fdc00-433">Bir dilim iki yolla yeniden çalıştırıldığında, aynı veri dilimi çalıştırmak kaç kez geçtiğinden bağımsız okuduğunuzdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdc00-433">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="fdc00-434">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="fdc00-434">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="fdc00-435">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="fdc00-435">Performance and Tuning</span></span>
<span data-ttu-id="fdc00-436">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve onu en iyi duruma getirmek için çeşitli yollar etkisi performansını anahtar Etkenler hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="fdc00-436">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
