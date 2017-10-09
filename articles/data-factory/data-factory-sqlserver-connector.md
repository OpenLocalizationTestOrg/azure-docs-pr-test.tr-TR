---
title: SQL Server'dan aaaMove veri tooand | Microsoft Docs
description: "Azure Data Factory kullanarak Azure VM'deki veya nasıl/SQL Server toomove verileri şirket içi yani veritabanı hakkında bilgi edinin."
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
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="96367-103">Azure Data Factory kullanarak veri tooand şirket içi SQL Server veya Iaas (Azure VM) üzerinde taşıma</span><span class="sxs-lookup"><span data-stu-id="96367-103">Move data tooand from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="96367-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove için/şirket içi SQL Server veritabanındaki verileri de açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="96367-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="96367-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="96367-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="96367-106">Desteklenen senaryolar</span><span class="sxs-lookup"><span data-stu-id="96367-106">Supported scenarios</span></span>
<span data-ttu-id="96367-107">Veri kopyalama **bir SQL Server veritabanından** veri depolarına aşağıdaki toohello:</span><span class="sxs-lookup"><span data-stu-id="96367-107">You can copy data **from a SQL Server database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="96367-108">Veri depoları aşağıdaki hello verileri kopyalayabilirsiniz **tooa SQL Server veritabanı**:</span><span class="sxs-lookup"><span data-stu-id="96367-108">You can copy data from hello following data stores **tooa SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="96367-109">Desteklenen SQL Server sürümleri</span><span class="sxs-lookup"><span data-stu-id="96367-109">Supported SQL Server versions</span></span>
<span data-ttu-id="96367-110">Verileri kopyalama bu SQL Server bağlayıcı desteği / toohello aşağıdaki sürümler barındırılan örneği şirket içi veya Azure SQL kimlik doğrulaması ve Windows kimlik doğrulaması kullanarak Iaas: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="96367-110">This SQL Server connector support copying data from/toohello following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="96367-111">Bağlantıyı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="96367-111">Enabling connectivity</span></span>
<span data-ttu-id="96367-112">Merhaba kavramlar ve SQL Server barındırılan şirket içi veya Azure Iaas VM'ler (altyapı-bir hizmet olarak) bağlanmak için gereken adımlar şunlardır hello aynı.</span><span class="sxs-lookup"><span data-stu-id="96367-112">hello concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are hello same.</span></span> <span data-ttu-id="96367-113">Her iki durumda da toouse veri yönetimi ağ geçidi bağlantısı için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="96367-113">In both cases, you need toouse Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="96367-114">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale toolearn veri yönetimi ağ geçidi ve hello ağ geçidi kurun ayarlama hakkında adım adım yönergeleri hakkında.</span><span class="sxs-lookup"><span data-stu-id="96367-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="96367-115">Bir ağ geçidi örneği SQL Server ile bağlanmak için bir önkoşul ayardır.</span><span class="sxs-lookup"><span data-stu-id="96367-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="96367-116">Ağ geçidi yüklenirken hello üzerinde aynı makine veya Bulut VM örneği daha iyi performans için SQL Server hello gibi şirket içi, bunları farklı makinelere yüklemeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="96367-116">While you can install gateway on hello same on-premises machine or cloud VM instance as hello SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="96367-117">Merhaba ağ geçidi ve SQL Server ayrı makinelerde sahip kaynak çekişmesini azaltır.</span><span class="sxs-lookup"><span data-stu-id="96367-117">Having hello gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="96367-118">Başlarken</span><span class="sxs-lookup"><span data-stu-id="96367-118">Getting started</span></span>
<span data-ttu-id="96367-119">Farklı araçlar/API'lerini kullanarak bir şirket içi SQL Server veritabanından/gelen verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="96367-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="96367-120">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="96367-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="96367-121">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="96367-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="96367-122">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="96367-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="96367-123">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="96367-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="96367-124">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="96367-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="96367-125">Oluşturma bir **veri fabrikası**.</span><span class="sxs-lookup"><span data-stu-id="96367-125">Create a **data factory**.</span></span> <span data-ttu-id="96367-126">Veri Fabrikası bir veya daha fazla ardışık düzen içerebilir.</span><span class="sxs-lookup"><span data-stu-id="96367-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="96367-127">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="96367-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="96367-128">Bir SQL Server veritabanı tooan Azure blob depolama veri kopyalama, örneğin, iki bağlı hizmet toolink SQL Server veritabanı ve Azure depolama hesabı tooyour veri fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="96367-128">For example, if you are copying data from a SQL Server database tooan Azure blob storage, you create two linked services toolink your SQL Server database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="96367-129">Belirli tooSQL Server veritabanına bağlı hizmet özellikler için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="96367-129">For linked service properties that are specific tooSQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="96367-130">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="96367-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="96367-131">Merhaba son adımda bahsedilen hello örnekte, SQL Server veritabanınız hello giriş verileri içeren bir veri kümesi toospecify hello SQL tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="96367-131">In hello example mentioned in hello last step, you create a dataset toospecify hello SQL table in your SQL Server database that contains hello input data.</span></span> <span data-ttu-id="96367-132">Başka bir veri kümesi toospecify hello blob kapsayıcı oluşturun ve hello verilerini tutan hello klasörü hello SQL Server veritabanı kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="96367-132">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello SQL Server database.</span></span> <span data-ttu-id="96367-133">Belirli tooSQL Server veritabanı veri kümesi özellikleri için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="96367-133">For dataset properties that are specific tooSQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="96367-134">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="96367-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="96367-135">Daha önce bahsedilen hello örnekte SqlSource bir kaynak ve BlobSink havuzu olarak hello kopya etkinliği için kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="96367-135">In hello example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="96367-136">Azure Blob Storage tooSQL sunucu veritabanı kopyalıyorsanız benzer şekilde, BlobSource ve SqlSink hello kopyalama etkinliği kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="96367-136">Similarly, if you are copying from Azure Blob Storage tooSQL Server Database, you use BlobSource and SqlSink in hello copy activity.</span></span> <span data-ttu-id="96367-137">Belirli tooSQL sunucu veritabanı kopyalama etkinliği özellikler için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="96367-137">For copy activity properties that are specific tooSQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="96367-138">Nasıl toouse bir veri deposu bir kaynak veya bir havuz olarak hakkında daha fazla bilgi için veri deposu hello önceki bölümdeki hello bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="96367-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="96367-139">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="96367-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="96367-140">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="96367-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="96367-141">Bir şirket içi SQL Server veritabanı/kullanılan toocopy verileri olan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples-for-copying-data-from-and-to-sql-server) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="96367-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="96367-142">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooSQL sunucu olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="96367-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="96367-143">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="96367-143">Linked service properties</span></span>
<span data-ttu-id="96367-144">Bağlı hizmet türü oluşturma **OnPremisesSqlServer** toolink bir şirket içi SQL Server veritabanı tooa data factory.</span><span class="sxs-lookup"><span data-stu-id="96367-144">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="96367-145">Aşağıdaki tablonun hello JSON öğeleri belirli tooon şirket içi SQL Server bağlantılı hizmet açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="96367-145">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="96367-146">Aşağıdaki tablonun hello JSON öğeleri belirli tooSQL Server bağlantılı hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="96367-146">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="96367-147">Özellik</span><span class="sxs-lookup"><span data-stu-id="96367-147">Property</span></span> | <span data-ttu-id="96367-148">Açıklama</span><span class="sxs-lookup"><span data-stu-id="96367-148">Description</span></span> | <span data-ttu-id="96367-149">Gerekli</span><span class="sxs-lookup"><span data-stu-id="96367-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="96367-150">type</span><span class="sxs-lookup"><span data-stu-id="96367-150">type</span></span> |<span data-ttu-id="96367-151">Merhaba type özelliği ayarlanmalıdır: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="96367-151">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="96367-152">Evet</span><span class="sxs-lookup"><span data-stu-id="96367-152">Yes</span></span> |
| <span data-ttu-id="96367-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="96367-153">connectionString</span></span> |<span data-ttu-id="96367-154">SQL kimlik doğrulaması veya Windows kimlik doğrulaması kullanarak tooconnect toohello şirket içi SQL Server veritabanı gerekli connectionString bilgiler belirtin.</span><span class="sxs-lookup"><span data-stu-id="96367-154">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="96367-155">Evet</span><span class="sxs-lookup"><span data-stu-id="96367-155">Yes</span></span> |
| <span data-ttu-id="96367-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="96367-156">gatewayName</span></span> |<span data-ttu-id="96367-157">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi SQL Server veritabanını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="96367-157">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="96367-158">Evet</span><span class="sxs-lookup"><span data-stu-id="96367-158">Yes</span></span> |
| <span data-ttu-id="96367-159">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="96367-159">username</span></span> |<span data-ttu-id="96367-160">Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="96367-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="96367-161">Örnek: **domainname\\kullanıcıadı**.</span><span class="sxs-lookup"><span data-stu-id="96367-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="96367-162">Hayır</span><span class="sxs-lookup"><span data-stu-id="96367-162">No</span></span> |
| <span data-ttu-id="96367-163">password</span><span class="sxs-lookup"><span data-stu-id="96367-163">password</span></span> |<span data-ttu-id="96367-164">Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="96367-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="96367-165">Hayır</span><span class="sxs-lookup"><span data-stu-id="96367-165">No</span></span> |

<span data-ttu-id="96367-166">Hello kullanarak kimlik bilgilerini şifrelemek **yeni AzureRmDataFactoryEncryptValue** cmdlet'i ve bunları hello aşağıdaki örnekte gösterildiği gibi hello bağlantı dizesinde kullanabilirsiniz (**EncryptedCredential** özellik):</span><span class="sxs-lookup"><span data-stu-id="96367-166">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="96367-167">Örnekler</span><span class="sxs-lookup"><span data-stu-id="96367-167">Samples</span></span>
<span data-ttu-id="96367-168">**SQL kimlik doğrulaması kullanarak JSON**</span><span class="sxs-lookup"><span data-stu-id="96367-168">**JSON for using SQL Authentication**</span></span>

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
<span data-ttu-id="96367-169">**Windows kimlik doğrulaması kullanmak için JSON**</span><span class="sxs-lookup"><span data-stu-id="96367-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="96367-170">Veri Yönetimi ağ geçidi kimliğine bürünmek hello belirtilen kullanıcı hesabı tooconnect toohello şirket içi SQL Server veritabanı.</span><span class="sxs-lookup"><span data-stu-id="96367-170">Data Management Gateway will impersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> 

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

## <a name="dataset-properties"></a><span data-ttu-id="96367-171">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="96367-171">Dataset properties</span></span>
<span data-ttu-id="96367-172">Bir veri türünde kullanılan Hello örneklerinde **SqlServerTable** toorepresent bir SQL Server veritabanındaki bir tablo.</span><span class="sxs-lookup"><span data-stu-id="96367-172">In hello samples, you have used a dataset of type **SqlServerTable** toorepresent a table in a SQL Server database.</span></span>  

<span data-ttu-id="96367-173">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="96367-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="96367-174">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (SQL Server, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="96367-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="96367-175">Merhaba typeProperties bölümü veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="96367-175">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="96367-176">Merhaba **typeProperties** hello veri kümesi için bir bölüm türü **SqlServerTable** hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="96367-176">hello **typeProperties** section for hello dataset of type **SqlServerTable** has hello following properties:</span></span>

| <span data-ttu-id="96367-177">Özellik</span><span class="sxs-lookup"><span data-stu-id="96367-177">Property</span></span> | <span data-ttu-id="96367-178">Açıklama</span><span class="sxs-lookup"><span data-stu-id="96367-178">Description</span></span> | <span data-ttu-id="96367-179">Gerekli</span><span class="sxs-lookup"><span data-stu-id="96367-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="96367-180">tableName</span><span class="sxs-lookup"><span data-stu-id="96367-180">tableName</span></span> |<span data-ttu-id="96367-181">Merhaba tablo veya Görünüm hizmeti bağlı hello SQL Server veritabanı örneğinde başvurduğu adı.</span><span class="sxs-lookup"><span data-stu-id="96367-181">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="96367-182">Evet</span><span class="sxs-lookup"><span data-stu-id="96367-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="96367-183">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="96367-183">Copy activity properties</span></span>
<span data-ttu-id="96367-184">Bir SQL Server veritabanından veri taşıyorsanız, hello kaynak türü hello kopyalama etkinliği çok ayarladığınız**SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="96367-184">If you are moving data from a SQL Server database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="96367-185">Veri tooa SQL Server veritabanını taşıyorsanız, benzer şekilde, hello Havuz türü hello kopyalama etkinliği çok ayarladığınız**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="96367-185">Similarly, if you are moving data tooa SQL Server database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="96367-186">Bu bölümde SqlSource ve SqlSink tarafından desteklenen özellikler listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="96367-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="96367-187">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="96367-187">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="96367-188">Ad, açıklama, giriş ve çıkış tabloları ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="96367-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="96367-189">Merhaba kopyalama etkinliği yalnızca bir girdi alır ve tek bir çıktı üretir.</span><span class="sxs-lookup"><span data-stu-id="96367-189">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="96367-190">Oysa hello typeProperties bölümünde hello etkinlik özellikleri her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="96367-190">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="96367-191">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="96367-191">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="96367-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="96367-192">SqlSource</span></span>
<span data-ttu-id="96367-193">Kopyalama etkinliği kaynağında türü olduğunda **SqlSource**, aşağıdaki özelliklere hello kullanılabilir **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="96367-193">When source in a copy activity is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="96367-194">Özellik</span><span class="sxs-lookup"><span data-stu-id="96367-194">Property</span></span> | <span data-ttu-id="96367-195">Açıklama</span><span class="sxs-lookup"><span data-stu-id="96367-195">Description</span></span> | <span data-ttu-id="96367-196">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="96367-196">Allowed values</span></span> | <span data-ttu-id="96367-197">Gerekli</span><span class="sxs-lookup"><span data-stu-id="96367-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="96367-198">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="96367-198">sqlReaderQuery</span></span> |<span data-ttu-id="96367-199">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="96367-199">Use hello custom query tooread data.</span></span> |<span data-ttu-id="96367-200">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="96367-200">SQL query string.</span></span> <span data-ttu-id="96367-201">Örneğin: seçin * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="96367-201">For example: select * from MyTable.</span></span> <span data-ttu-id="96367-202">Birden çok tablo hello girdi veri kümesi tarafından başvurulan hello veritabanından başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="96367-202">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="96367-203">Belirtilmezse, yürütülen SQL deyimini hello: MyTable arasından seçin.</span><span class="sxs-lookup"><span data-stu-id="96367-203">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="96367-204">Hayır</span><span class="sxs-lookup"><span data-stu-id="96367-204">No</span></span> |
| <span data-ttu-id="96367-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="96367-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="96367-206">Merhaba adını hello kaynak tablodan veri okuyan yordamı depolanır.</span><span class="sxs-lookup"><span data-stu-id="96367-206">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="96367-207">Saklı yordam hello adı.</span><span class="sxs-lookup"><span data-stu-id="96367-207">Name of hello stored procedure.</span></span> <span data-ttu-id="96367-208">Merhaba son SQL deyimi SELECT deyimi hello saklı yordam içinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="96367-208">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="96367-209">Hayır</span><span class="sxs-lookup"><span data-stu-id="96367-209">No</span></span> |
| <span data-ttu-id="96367-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="96367-210">storedProcedureParameters</span></span> |<span data-ttu-id="96367-211">Saklı yordam hello için parametreler.</span><span class="sxs-lookup"><span data-stu-id="96367-211">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="96367-212">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="96367-212">Name/value pairs.</span></span> <span data-ttu-id="96367-213">Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="96367-213">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="96367-214">Hayır</span><span class="sxs-lookup"><span data-stu-id="96367-214">No</span></span> |

<span data-ttu-id="96367-215">Merhaba, **sqlReaderQuery** Merhaba SqlSource, hello kopyalama etkinliği çalıştıran bu sorguyu hello SQL Server veritabanı kaynak tooget hello verileri karşı belirtilir.</span><span class="sxs-lookup"><span data-stu-id="96367-215">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="96367-216">Alternatif olarak, bir saklı yordam hello belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (Merhaba saklı yordam parametreleri alır).</span><span class="sxs-lookup"><span data-stu-id="96367-216">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="96367-217">SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz hello yapısı bölümünde tanımlanan hello sütunlar kullanılan toobuild seçme sorgusu toorun hello SQL Server veritabanına karşı'dır.</span><span class="sxs-lookup"><span data-stu-id="96367-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="96367-218">Merhaba veri kümesi tanımı hello yapısına sahip değil, tüm sütunlar hello tablosundan seçilir.</span><span class="sxs-lookup"><span data-stu-id="96367-218">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="96367-219">Kullandığınızda, **sqlReaderStoredProcedureName**, hala toospecify bir değer hello için gereksinim duyduğunuz **tableName** JSON hello kümesindeki özelliği.</span><span class="sxs-lookup"><span data-stu-id="96367-219">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="96367-220">Yine de bu tabloya karşı gerçekleştirilen başka doğrulama vardır.</span><span class="sxs-lookup"><span data-stu-id="96367-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="96367-221">SqlSink</span><span class="sxs-lookup"><span data-stu-id="96367-221">SqlSink</span></span>
<span data-ttu-id="96367-222">**SqlSink** aşağıdaki özelliklere hello destekler:</span><span class="sxs-lookup"><span data-stu-id="96367-222">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="96367-223">Özellik</span><span class="sxs-lookup"><span data-stu-id="96367-223">Property</span></span> | <span data-ttu-id="96367-224">Açıklama</span><span class="sxs-lookup"><span data-stu-id="96367-224">Description</span></span> | <span data-ttu-id="96367-225">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="96367-225">Allowed values</span></span> | <span data-ttu-id="96367-226">Gerekli</span><span class="sxs-lookup"><span data-stu-id="96367-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="96367-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="96367-227">writeBatchTimeout</span></span> |<span data-ttu-id="96367-228">Zaman aşımına uğramadan önce hello toplu ekleme işlemi toocomplete bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="96367-228">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="96367-229">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="96367-229">timespan</span></span><br/><br/> <span data-ttu-id="96367-230">Örnek: "00: 30:00" (30 dakika).</span><span class="sxs-lookup"><span data-stu-id="96367-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="96367-231">Hayır</span><span class="sxs-lookup"><span data-stu-id="96367-231">No</span></span> |
| <span data-ttu-id="96367-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="96367-232">writeBatchSize</span></span> |<span data-ttu-id="96367-233">Merhaba arabellek boyutu writeBatchSize ulaştığında veri hello SQL tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="96367-233">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="96367-234">Tamsayı (satır sayısı)</span><span class="sxs-lookup"><span data-stu-id="96367-234">Integer (number of rows)</span></span> |<span data-ttu-id="96367-235">Hayır (varsayılan: 10000)</span><span class="sxs-lookup"><span data-stu-id="96367-235">No (default: 10000)</span></span> |
| <span data-ttu-id="96367-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="96367-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="96367-237">Belirli bir dilimle verilerinin temizlenmesini gibi kopyalama etkinliği tooexecute için sorgu belirtin.</span><span class="sxs-lookup"><span data-stu-id="96367-237">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="96367-238">Daha fazla bilgi için bkz: [yinelenebilir kopyalama](#repeatable-copy) bölümü.</span><span class="sxs-lookup"><span data-stu-id="96367-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="96367-239">Sorgu bildirimi.</span><span class="sxs-lookup"><span data-stu-id="96367-239">A query statement.</span></span> |<span data-ttu-id="96367-240">Hayır</span><span class="sxs-lookup"><span data-stu-id="96367-240">No</span></span> |
| <span data-ttu-id="96367-241">Sliceıdentifiercolumnname</span><span class="sxs-lookup"><span data-stu-id="96367-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="96367-242">Kopyalama etkinliği toofill sütun adı, ne zaman yeniden çalıştırılacağını belirli bir dilim verilerini kullanılan tooclean olduğu otomatik dilim tanımlayıcı ile belirtin.</span><span class="sxs-lookup"><span data-stu-id="96367-242">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="96367-243">Daha fazla bilgi için bkz: [yinelenebilir kopyalama](#repeatable-copy) bölümü.</span><span class="sxs-lookup"><span data-stu-id="96367-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="96367-244">Binary(32) veri türüne sahip bir sütunun sütun adı.</span><span class="sxs-lookup"><span data-stu-id="96367-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="96367-245">Hayır</span><span class="sxs-lookup"><span data-stu-id="96367-245">No</span></span> |
| <span data-ttu-id="96367-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="96367-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="96367-247">Merhaba adını upserts (güncelleştirmeler/ekler) verileri hello hedef tabloya saklı yordamı.</span><span class="sxs-lookup"><span data-stu-id="96367-247">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="96367-248">Saklı yordam hello adı.</span><span class="sxs-lookup"><span data-stu-id="96367-248">Name of hello stored procedure.</span></span> |<span data-ttu-id="96367-249">Hayır</span><span class="sxs-lookup"><span data-stu-id="96367-249">No</span></span> |
| <span data-ttu-id="96367-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="96367-250">storedProcedureParameters</span></span> |<span data-ttu-id="96367-251">Saklı yordam hello için parametreler.</span><span class="sxs-lookup"><span data-stu-id="96367-251">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="96367-252">Ad/değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="96367-252">Name/value pairs.</span></span> <span data-ttu-id="96367-253">Adları ve büyük/küçük harf parametrelerinin hello adları ve büyük küçük harf kullanımını hello saklı yordam parametreleri eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="96367-253">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="96367-254">Hayır</span><span class="sxs-lookup"><span data-stu-id="96367-254">No</span></span> |
| <span data-ttu-id="96367-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="96367-255">sqlWriterTableType</span></span> |<span data-ttu-id="96367-256">Merhaba saklı yordamda kullanılan tablo türü adı toobe belirtin.</span><span class="sxs-lookup"><span data-stu-id="96367-256">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="96367-257">Kopyalama etkinliği taşınan hello veri geçici bir tablo bu tablo türü ile kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="96367-257">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="96367-258">Saklı yordam kodu sonra varolan verilerin kopyalanmasını hello verileri birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96367-258">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="96367-259">Bir tablo türü adı.</span><span class="sxs-lookup"><span data-stu-id="96367-259">A table type name.</span></span> |<span data-ttu-id="96367-260">Hayır</span><span class="sxs-lookup"><span data-stu-id="96367-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a><span data-ttu-id="96367-261">Verileri ve tooSQL sunucu kopyalamak için JSON örnekleri</span><span class="sxs-lookup"><span data-stu-id="96367-261">JSON examples for copying data from and tooSQL Server</span></span>
<span data-ttu-id="96367-262">Merhaba aşağıdaki örneklerde sağlayan örnek JSON tanımları toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="96367-262">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="96367-263">Örnekleri göster nasıl aşağıdaki hello toocopy veri tooand SQL Server ve Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="96367-263">hello following samples show how toocopy data tooand from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="96367-264">Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden belirtildiği hello havuzlarını, kaynakları tooany [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="96367-264">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a><span data-ttu-id="96367-265">Örnek: Verilerini SQL Server tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="96367-265">Example: Copy data from SQL Server tooAzure Blob</span></span>
<span data-ttu-id="96367-266">Merhaba, aşağıdaki örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="96367-266">hello following sample shows:</span></span>

1. <span data-ttu-id="96367-267">Bağlı hizmet türü [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="96367-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="96367-268">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="96367-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="96367-269">Bir giriş [dataset](data-factory-create-datasets.md) türü [SqlServerTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="96367-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="96367-270">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="96367-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="96367-271">Merhaba [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [SqlSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="96367-271">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="96367-272">Merhaba örnek time series verilerini bir SQL Server tablo tooan Azure blob saatte kopyalar.</span><span class="sxs-lookup"><span data-stu-id="96367-272">hello sample copies time-series data from a SQL Server table tooan Azure blob every hour.</span></span> <span data-ttu-id="96367-273">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="96367-273">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="96367-274">İlk adım olarak, hello veri yönetimi ağ geçidi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="96367-274">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="96367-275">Merhaba yönergelerdir hello [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="96367-275">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="96367-276">**SQL Server bağlantılı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="96367-276">**SQL Server linked service**</span></span>
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
<span data-ttu-id="96367-277">**Azure Blob storage bağlı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="96367-277">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="96367-278">**SQL Server girdi veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="96367-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="96367-279">Merhaba örnek SQL Server'da bir tablo "MyTable" oluşturulur ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="96367-279">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="96367-280">Tek bir veri kümesi, ancak tek bir tabloyu kullanarak aynı veritabanı hello veri kümesi'nin tableName typeProperty için kullanılması gereken hello içinde birden çok tablo üzerinde sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96367-280">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="96367-281">"Dış" ayarı: "true" bildirir Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="96367-281">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="96367-282">**Azure Blob dataset çıktı**</span><span class="sxs-lookup"><span data-stu-id="96367-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="96367-283">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="96367-283">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="96367-284">hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="96367-284">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="96367-285">Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="96367-285">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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
<span data-ttu-id="96367-286">**Kopyalama etkinliği ile kanalı**</span><span class="sxs-lookup"><span data-stu-id="96367-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="96367-287">Merhaba ardışık düzen içeren bir kopyalama etkinliği, yapılandırılmış toouse bu girdi ve çıktı veri kümeleri ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="96367-287">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="96367-288">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**SqlSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="96367-288">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="96367-289">Merhaba belirtilen hello SQL sorgusu **SqlReaderQuery** özelliği saat toocopy geçmiş hello hello veri seçer.</span><span class="sxs-lookup"><span data-stu-id="96367-289">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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
<span data-ttu-id="96367-290">Bu örnekte, **sqlReaderQuery** SqlSource hello için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="96367-290">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="96367-291">Merhaba kopyalama etkinliği bu sorguyu SQL Server veritabanı kaynak tooget hello verileri hello karşı çalışır.</span><span class="sxs-lookup"><span data-stu-id="96367-291">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="96367-292">Alternatif olarak, bir saklı yordam hello belirterek belirleyebileceğiniz **sqlReaderStoredProcedureName** ve **storedProcedureParameters** (Merhaba saklı yordam parametreleri alır).</span><span class="sxs-lookup"><span data-stu-id="96367-292">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="96367-293">Merhaba sqlReaderQuery hello girdi veri kümesi tarafından başvurulan hello veritabanı içinde birden çok tablo başvuruda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="96367-293">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="96367-294">Bu veri kümesi'nin tableName typeProperty hello olarak ayarlanmış sınırlı tooonly hello tablosu değil.</span><span class="sxs-lookup"><span data-stu-id="96367-294">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="96367-295">SqlReaderQuery veya sqlReaderStoredProcedureName belirtmezseniz hello yapısı bölümünde tanımlanan hello sütunlar kullanılan toobuild seçme sorgusu toorun hello SQL Server veritabanına karşı'dır.</span><span class="sxs-lookup"><span data-stu-id="96367-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="96367-296">Merhaba veri kümesi tanımı hello yapısına sahip değil, tüm sütunlar hello tablosundan seçilir.</span><span class="sxs-lookup"><span data-stu-id="96367-296">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="96367-297">Hello bkz [Sql kaynağı](#sqlsource) bölüm ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) SqlSource ve BlobSink tarafından desteklenen özellikler hello listesi.</span><span class="sxs-lookup"><span data-stu-id="96367-297">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-toosql-server"></a><span data-ttu-id="96367-298">Örnek: Kopyalama verileri Azure Blob tooSQL sunucu</span><span class="sxs-lookup"><span data-stu-id="96367-298">Example: Copy data from Azure Blob tooSQL Server</span></span>
<span data-ttu-id="96367-299">Merhaba, aşağıdaki örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="96367-299">hello following sample shows:</span></span>

1. <span data-ttu-id="96367-300">Merhaba bağlantılı hizmet türü [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="96367-300">hello linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="96367-301">Merhaba bağlantılı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="96367-301">hello linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="96367-302">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="96367-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="96367-303">Bir çıkış [dataset](data-factory-create-datasets.md) türü [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="96367-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="96367-304">Merhaba [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) ve [SqlSink](#sql-server-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="96367-304">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="96367-305">Merhaba örnek time series verilerini her saat bir Azure blob tooa SQL Server tablosundan kopyalar.</span><span class="sxs-lookup"><span data-stu-id="96367-305">hello sample copies time-series data from an Azure blob tooa SQL Server table every hour.</span></span> <span data-ttu-id="96367-306">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="96367-306">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="96367-307">**SQL Server bağlantılı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="96367-307">**SQL Server linked service**</span></span>

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
<span data-ttu-id="96367-308">**Azure Blob storage bağlı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="96367-308">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="96367-309">**Azure Blob girdi veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="96367-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="96367-310">Veri toplanma yeni blob üzerinden saatte (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="96367-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="96367-311">Merhaba klasör yolu ve dosya adını hello blob dinamik olarak değerlendirilir işleniyor hello dilimin hello başlangıç zamanı temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="96367-311">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="96367-312">Merhaba klasör yolu yıl, ay ve gün kısmını hello başlangıç saati ve dosya adı hello başlangıç saati hello saat bölümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="96367-312">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="96367-313">"dış": "true" ayarı bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil hello Data Factory hizmetinin sizi bilgilendirir.</span><span class="sxs-lookup"><span data-stu-id="96367-313">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="96367-314">**SQL Server çıktı veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="96367-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="96367-315">Merhaba örnek SQL Server'da "MyTable" olarak adlandırılan veri tooa tablosuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="96367-315">hello sample copies data tooa table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="96367-316">SQL Server ile Merhaba tablosunu oluşturan hello Blob CSV dosyası toocontain beklediğiniz gibi hello aynı sayıda sütun.</span><span class="sxs-lookup"><span data-stu-id="96367-316">Create hello table in SQL Server with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="96367-317">Yeni satırlar toohello tablo saatte eklenir.</span><span class="sxs-lookup"><span data-stu-id="96367-317">New rows are added toohello table every hour.</span></span>

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
<span data-ttu-id="96367-318">**Kopyalama etkinliği ile kanalı**</span><span class="sxs-lookup"><span data-stu-id="96367-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="96367-319">Merhaba ardışık düzen içeren bir kopyalama etkinliği, yapılandırılmış toouse bu girdi ve çıktı veri kümeleri ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="96367-319">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="96367-320">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**BlobSource** ve **havuz** türü olarak ayarlanmış çok**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="96367-320">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="96367-321">Bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="96367-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="96367-322">SQL Server tooaccept uzak bağlantıları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="96367-322">Configure your SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="96367-323">Başlatma **SQL Server Management Studio**, sağ **server**, tıklatıp **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="96367-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="96367-324">Seçin **bağlantıları** hello listesi ve onay **izin uzak bağlantıları toohello sunucu**.</span><span class="sxs-lookup"><span data-stu-id="96367-324">Select **Connections** from hello list and check **Allow remote connections toohello server**.</span></span>

    ![Uzak bağlantıları etkinleştir](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="96367-326">Bkz: [hello uzaktan erişim sunucu yapılandırma seçeneğini yapılandırma](https://msdn.microsoft.com/library/ms191464.aspx) ayrıntılı adımlar için.</span><span class="sxs-lookup"><span data-stu-id="96367-326">See [Configure hello remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="96367-327">Başlatma **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="96367-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="96367-328">Genişletme **SQL Server Ağ Yapılandırması** Merhaba istediğiniz ' nı seçip örnek **MSSQLSERVER protokolleri**.</span><span class="sxs-lookup"><span data-stu-id="96367-328">Expand **SQL Server Network Configuration** for hello instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="96367-329">Protokolleri hello sağ bölmesinde görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="96367-329">You should see protocols in hello right-pane.</span></span> <span data-ttu-id="96367-330">Sağ tıklayarak TCP/IP'yi etkinleştirin **TCP/IP'yi** tıklatıp **etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="96367-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![TCP/IP'yi etkinleştirin](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="96367-332">Bkz: [etkinleştirmek veya devre dışı bir sunucu ağ protokolü](https://msdn.microsoft.com/library/ms191294.aspx) ayrıntı ve TCP/IP protokolünün etkinleştirilmesi alternatif yolu.</span><span class="sxs-lookup"><span data-stu-id="96367-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="96367-333">Buna Merhaba aynı penceresi, çift **TCP/IP'yi** toolaunch **TCP/IP özelliklerini** penceresi.</span><span class="sxs-lookup"><span data-stu-id="96367-333">In hello same window, double-click **TCP/IP** toolaunch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="96367-334">Geçiş toohello **IP adreslerini** sekmesi. Toosee aşağı **IPAll** bölümü.</span><span class="sxs-lookup"><span data-stu-id="96367-334">Switch toohello **IP Addresses** tab. Scroll down toosee **IPAll** section.</span></span> <span data-ttu-id="96367-335">Merhaba Not ** TCP bağlantı noktası ** (varsayılan değer **1433**).</span><span class="sxs-lookup"><span data-stu-id="96367-335">Note down hello **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="96367-336">Oluşturma bir **hello Windows Güvenlik Duvarı Kuralı** hello makine tooallow Bu bağlantı noktası üzerinden gelen trafiği üzerinde.</span><span class="sxs-lookup"><span data-stu-id="96367-336">Create a **rule for hello Windows Firewall** on hello machine tooallow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="96367-337">**Bağlantıyı doğrulama**: tooconnect toohello tam adını kullanarak SQL Server başka bir makineden SQL Server Management Studio kullanın.</span><span class="sxs-lookup"><span data-stu-id="96367-337">**Verify connection**: tooconnect toohello SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="96367-338">Örneğin: "<machine>.<domain>. Corp.<company>.com, 1433. "</span><span class="sxs-lookup"><span data-stu-id="96367-338">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="96367-339">Bkz: [şirket içi kaynakları ve veri yönetimi ağ geçidi ile Merhaba bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="96367-339">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="96367-340">Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="96367-340">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="96367-341">Merhaba hedef veritabanında kimlik sütunu</span><span class="sxs-lookup"><span data-stu-id="96367-341">Identity columns in hello target database</span></span>
<span data-ttu-id="96367-342">Bu bölümde bir kimlik sütunu sahip bir kimlik sütunu tooa hedef tablo içeren bir kaynak tablo verileri kopyalar bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="96367-342">This section provides an example that copies data from a source table with no identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="96367-343">**Kaynak tablosu:**</span><span class="sxs-lookup"><span data-stu-id="96367-343">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="96367-344">**Hedef Tablo:**</span><span class="sxs-lookup"><span data-stu-id="96367-344">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="96367-345">Merhaba hedef tablosunun bir kimlik sütunu olan dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="96367-345">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="96367-346">**Kaynak veri kümesi JSON tanımı**</span><span class="sxs-lookup"><span data-stu-id="96367-346">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="96367-347">**Hedef veri kümesi JSON tanımı**</span><span class="sxs-lookup"><span data-stu-id="96367-347">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="96367-348">Kaynak ve hedef tablosu farklı şema sahip dikkat edin (hedef kimliğine sahip başka bir sütuna sahip).</span><span class="sxs-lookup"><span data-stu-id="96367-348">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="96367-349">Bu senaryoda, toospecify gerek **yapısı** hello kimlik sütunu içermeyen hello hedef veri kümesi tanımında özelliği.</span><span class="sxs-lookup"><span data-stu-id="96367-349">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="96367-350">SQL havuz depolanan yordamı çağırma</span><span class="sxs-lookup"><span data-stu-id="96367-350">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="96367-351">Bkz: [kopyalama etkinliği SQL havuz için saklı yordam çağırma](data-factory-invoke-stored-procedure-from-copy-activity.md) makale SQL havuz ardışık kopyalama etkinliğinde bir saklı yordam çağırma örneği.</span><span class="sxs-lookup"><span data-stu-id="96367-351">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="96367-352">Tür eşlemesi için SQL server</span><span class="sxs-lookup"><span data-stu-id="96367-352">Type mapping for SQL server</span></span>
<span data-ttu-id="96367-353">Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, hello kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri 2 adımlı yaklaşımı izleyerek hello ile:</span><span class="sxs-lookup"><span data-stu-id="96367-353">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="96367-354">Yerel kaynak türleri too.NET türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="96367-354">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="96367-355">.NET türü toonative havuz türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="96367-355">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="96367-356">Çok & SQL Server'dan veri taşımayı hello olduğunda aşağıdaki eşlemelerini too.NET türü ve bunun tersi de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="96367-356">When moving data too& from SQL server, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="96367-357">Merhaba eşleme hello ADO.NET için SQL Server veri türü eşlemesi olarak aynıdır.</span><span class="sxs-lookup"><span data-stu-id="96367-357">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="96367-358">SQL Server veritabanı altyapısı türü</span><span class="sxs-lookup"><span data-stu-id="96367-358">SQL Server Database Engine type</span></span> | <span data-ttu-id="96367-359">.NET framework türü</span><span class="sxs-lookup"><span data-stu-id="96367-359">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="96367-360">bigint</span><span class="sxs-lookup"><span data-stu-id="96367-360">bigint</span></span> |<span data-ttu-id="96367-361">Int64</span><span class="sxs-lookup"><span data-stu-id="96367-361">Int64</span></span> |
| <span data-ttu-id="96367-362">İkili</span><span class="sxs-lookup"><span data-stu-id="96367-362">binary</span></span> |<span data-ttu-id="96367-363">Byte]</span><span class="sxs-lookup"><span data-stu-id="96367-363">Byte[]</span></span> |
| <span data-ttu-id="96367-364">bit</span><span class="sxs-lookup"><span data-stu-id="96367-364">bit</span></span> |<span data-ttu-id="96367-365">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="96367-365">Boolean</span></span> |
| <span data-ttu-id="96367-366">char</span><span class="sxs-lookup"><span data-stu-id="96367-366">char</span></span> |<span data-ttu-id="96367-367">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="96367-367">String, Char[]</span></span> |
| <span data-ttu-id="96367-368">Tarih</span><span class="sxs-lookup"><span data-stu-id="96367-368">date</span></span> |<span data-ttu-id="96367-369">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="96367-369">DateTime</span></span> |
| <span data-ttu-id="96367-370">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="96367-370">Datetime</span></span> |<span data-ttu-id="96367-371">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="96367-371">DateTime</span></span> |
| <span data-ttu-id="96367-372">datetime2</span><span class="sxs-lookup"><span data-stu-id="96367-372">datetime2</span></span> |<span data-ttu-id="96367-373">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="96367-373">DateTime</span></span> |
| <span data-ttu-id="96367-374">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="96367-374">Datetimeoffset</span></span> |<span data-ttu-id="96367-375">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="96367-375">DateTimeOffset</span></span> |
| <span data-ttu-id="96367-376">Ondalık</span><span class="sxs-lookup"><span data-stu-id="96367-376">Decimal</span></span> |<span data-ttu-id="96367-377">Ondalık</span><span class="sxs-lookup"><span data-stu-id="96367-377">Decimal</span></span> |
| <span data-ttu-id="96367-378">FILESTREAM özniteliği (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="96367-378">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="96367-379">Byte]</span><span class="sxs-lookup"><span data-stu-id="96367-379">Byte[]</span></span> |
| <span data-ttu-id="96367-380">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="96367-380">Float</span></span> |<span data-ttu-id="96367-381">Çift</span><span class="sxs-lookup"><span data-stu-id="96367-381">Double</span></span> |
| <span data-ttu-id="96367-382">Görüntü</span><span class="sxs-lookup"><span data-stu-id="96367-382">image</span></span> |<span data-ttu-id="96367-383">Byte]</span><span class="sxs-lookup"><span data-stu-id="96367-383">Byte[]</span></span> |
| <span data-ttu-id="96367-384">Int</span><span class="sxs-lookup"><span data-stu-id="96367-384">int</span></span> |<span data-ttu-id="96367-385">Int32</span><span class="sxs-lookup"><span data-stu-id="96367-385">Int32</span></span> |
| <span data-ttu-id="96367-386">para</span><span class="sxs-lookup"><span data-stu-id="96367-386">money</span></span> |<span data-ttu-id="96367-387">Ondalık</span><span class="sxs-lookup"><span data-stu-id="96367-387">Decimal</span></span> |
| <span data-ttu-id="96367-388">nchar</span><span class="sxs-lookup"><span data-stu-id="96367-388">nchar</span></span> |<span data-ttu-id="96367-389">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="96367-389">String, Char[]</span></span> |
| <span data-ttu-id="96367-390">ntext</span><span class="sxs-lookup"><span data-stu-id="96367-390">ntext</span></span> |<span data-ttu-id="96367-391">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="96367-391">String, Char[]</span></span> |
| <span data-ttu-id="96367-392">sayısal</span><span class="sxs-lookup"><span data-stu-id="96367-392">numeric</span></span> |<span data-ttu-id="96367-393">Ondalık</span><span class="sxs-lookup"><span data-stu-id="96367-393">Decimal</span></span> |
| <span data-ttu-id="96367-394">nvarchar</span><span class="sxs-lookup"><span data-stu-id="96367-394">nvarchar</span></span> |<span data-ttu-id="96367-395">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="96367-395">String, Char[]</span></span> |
| <span data-ttu-id="96367-396">Gerçek</span><span class="sxs-lookup"><span data-stu-id="96367-396">real</span></span> |<span data-ttu-id="96367-397">Tek</span><span class="sxs-lookup"><span data-stu-id="96367-397">Single</span></span> |
| <span data-ttu-id="96367-398">rowVersion</span><span class="sxs-lookup"><span data-stu-id="96367-398">rowversion</span></span> |<span data-ttu-id="96367-399">Byte]</span><span class="sxs-lookup"><span data-stu-id="96367-399">Byte[]</span></span> |
| <span data-ttu-id="96367-400">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="96367-400">smalldatetime</span></span> |<span data-ttu-id="96367-401">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="96367-401">DateTime</span></span> |
| <span data-ttu-id="96367-402">tamsayı</span><span class="sxs-lookup"><span data-stu-id="96367-402">smallint</span></span> |<span data-ttu-id="96367-403">Int16</span><span class="sxs-lookup"><span data-stu-id="96367-403">Int16</span></span> |
| <span data-ttu-id="96367-404">küçük para</span><span class="sxs-lookup"><span data-stu-id="96367-404">smallmoney</span></span> |<span data-ttu-id="96367-405">Ondalık</span><span class="sxs-lookup"><span data-stu-id="96367-405">Decimal</span></span> |
| <span data-ttu-id="96367-406">sql_variant</span><span class="sxs-lookup"><span data-stu-id="96367-406">sql_variant</span></span> |<span data-ttu-id="96367-407">Nesne *</span><span class="sxs-lookup"><span data-stu-id="96367-407">Object *</span></span> |
| <span data-ttu-id="96367-408">Metin</span><span class="sxs-lookup"><span data-stu-id="96367-408">text</span></span> |<span data-ttu-id="96367-409">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="96367-409">String, Char[]</span></span> |
| <span data-ttu-id="96367-410">time</span><span class="sxs-lookup"><span data-stu-id="96367-410">time</span></span> |<span data-ttu-id="96367-411">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="96367-411">TimeSpan</span></span> |
| <span data-ttu-id="96367-412">timestamp</span><span class="sxs-lookup"><span data-stu-id="96367-412">timestamp</span></span> |<span data-ttu-id="96367-413">Byte]</span><span class="sxs-lookup"><span data-stu-id="96367-413">Byte[]</span></span> |
| <span data-ttu-id="96367-414">Mini tamsayı</span><span class="sxs-lookup"><span data-stu-id="96367-414">tinyint</span></span> |<span data-ttu-id="96367-415">Bayt</span><span class="sxs-lookup"><span data-stu-id="96367-415">Byte</span></span> |
| <span data-ttu-id="96367-416">benzersiz tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="96367-416">uniqueidentifier</span></span> |<span data-ttu-id="96367-417">GUID</span><span class="sxs-lookup"><span data-stu-id="96367-417">Guid</span></span> |
| <span data-ttu-id="96367-418">varbinary</span><span class="sxs-lookup"><span data-stu-id="96367-418">varbinary</span></span> |<span data-ttu-id="96367-419">Byte]</span><span class="sxs-lookup"><span data-stu-id="96367-419">Byte[]</span></span> |
| <span data-ttu-id="96367-420">varchar</span><span class="sxs-lookup"><span data-stu-id="96367-420">varchar</span></span> |<span data-ttu-id="96367-421">Dize, Char]</span><span class="sxs-lookup"><span data-stu-id="96367-421">String, Char[]</span></span> |
| <span data-ttu-id="96367-422">xml</span><span class="sxs-lookup"><span data-stu-id="96367-422">xml</span></span> |<span data-ttu-id="96367-423">XML</span><span class="sxs-lookup"><span data-stu-id="96367-423">Xml</span></span> |

## <a name="mapping-source-toosink-columns"></a><span data-ttu-id="96367-424">Kaynak toosink sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="96367-424">Mapping source toosink columns</span></span>
<span data-ttu-id="96367-425">Kaynak veri kümesi toocolumns havuz kümesinden toomap sütunlarından bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="96367-425">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="96367-426">Yinelenebilir kopyalama</span><span class="sxs-lookup"><span data-stu-id="96367-426">Repeatable copy</span></span>
<span data-ttu-id="96367-427">Veri tooSQL sunucu veritabanı kopyalama işlemi sırasında hello kopyalama etkinliği varsayılan olarak veri toohello havuz tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="96367-427">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="96367-428">Bunun yerine, tooperform bir UPSERT bkz [yinelenebilir yazma tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) makalesi.</span><span class="sxs-lookup"><span data-stu-id="96367-428">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="96367-429">İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları.</span><span class="sxs-lookup"><span data-stu-id="96367-429">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="96367-430">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96367-430">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="96367-431">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96367-431">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="96367-432">Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="96367-432">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="96367-433">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="96367-433">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="96367-434">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="96367-434">Performance and Tuning</span></span>
<span data-ttu-id="96367-435">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="96367-435">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
