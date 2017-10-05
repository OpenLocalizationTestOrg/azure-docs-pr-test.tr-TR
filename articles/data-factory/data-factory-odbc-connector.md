---
title: "ODBC veri depolarına veri taşıma | Microsoft Docs"
description: "Azure Data Factory kullanarak ODBC veri depolarını veri taşıma hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 269d9802ca4a6a16dbf9021929fe21104cb431f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="9b6fb-103">Azure Data Factory kullanarak veri öğesinden ODBC veri depolarını taşıma</span><span class="sxs-lookup"><span data-stu-id="9b6fb-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="9b6fb-104">Bu makalede kopya etkinliği Azure Data Factory'de bir şirket içi ODBC veri deposundan verileri taşımak için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises ODBC data store.</span></span> <span data-ttu-id="9b6fb-105">Derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) kopyalama etkinliği ile veri taşıma için genel bir bakış sunar makalesi.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="9b6fb-106">Bir ODBC veri deposundan verileri herhangi bir desteklenen havuz veri deposuna kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-106">You can copy data from an ODBC data store to any supported sink data store.</span></span> <span data-ttu-id="9b6fb-107">Veri depoları havuzlarını kopyalama etkinliği tarafından desteklenen bir listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="9b6fb-108">Veri Fabrikası şu anda yalnızca veri taşımayı bir ODBC veri deposundaki diğer veri depolarına, ancak verileri diğer veri depolarına bir ODBC veri deposuna taşıma değil destekler.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-108">Data factory currently supports only moving data from an ODBC data store to other data stores, but not for moving data from other data stores to an ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="9b6fb-109">Bağlantıyı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="9b6fb-109">Enabling connectivity</span></span>
<span data-ttu-id="9b6fb-110">Data Factory hizmetinin şirket içi ODBC kaynaklarına veri yönetimi ağ geçidi kullanarak bağlanmayı desteklemektedir.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-110">Data Factory service supports connecting to on-premises ODBC sources using the Data Management Gateway.</span></span> <span data-ttu-id="9b6fb-111">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale veri yönetimi ağ geçidi ve ağ geçidi kurun ayarlama hakkında adım adım yönergeleri hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="9b6fb-112">Bir Azure Iaas sanal barındırılan olsa bile bir ODBC veri deposuna bağlanmak için ağ geçidi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-112">Use the gateway to connect to an ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="9b6fb-113">ODBC veri deposu olarak aynı şirket içi makineye veya Azure VM ağ geçidi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-113">You can install the gateway on the same on-premises machine or the Azure VM as the ODBC data store.</span></span> <span data-ttu-id="9b6fb-114">Ancak, bir ayrı makine/Azure Iaas kaynak çekişmesini önlemek için VM üzerinde ve daha iyi performans için ağ geçidi yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-114">However, we recommend that you install the gateway on a separate machine/Azure IaaS VM to avoid resource contention and for better performance.</span></span> <span data-ttu-id="9b6fb-115">Ağ geçidi ayrı bir makineye yüklediğinizde, makine ODBC veri deposu olan makine erişebilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-115">When you install the gateway on a separate machine, the machine should be able to access the machine with the ODBC data store.</span></span>

<span data-ttu-id="9b6fb-116">Veri Yönetimi ağ geçidi dışında Ayrıca ağ geçidi makinesi üzerinde veri deposu için ODBC sürücüsü yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-116">Apart from the Data Management Gateway, you also need to install the ODBC driver for the data store on the gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="9b6fb-117">Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="9b6fb-118">Başlarken</span><span class="sxs-lookup"><span data-stu-id="9b6fb-118">Getting started</span></span>
<span data-ttu-id="9b6fb-119">Farklı araçlar/API'lerini kullanarak bir ODBC veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="9b6fb-120">Bir işlem hattı oluşturmak için en kolay yolu kullanmaktır **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="9b6fb-121">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) veri kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="9b6fb-122">Bir işlem hattı oluşturmak için aşağıdaki araçları kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu**, **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="9b6fb-123">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="9b6fb-124">Araçlar ya da API'leri kullanıp bir havuz veri deposu için bir kaynak veri deposundan verileri taşır bir ardışık düzen oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9b6fb-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="9b6fb-125">Oluşturma **bağlantılı Hizmetleri** girdi ve çıktı verilerini bağlamak için veri fabrikanıza depolar.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="9b6fb-126">Oluşturma **veri kümeleri** kopyalama işlemi için girdi ve çıktı verilerini temsil etmek için.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="9b6fb-127">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="9b6fb-128">Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="9b6fb-129">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, JSON biçimini kullanarak bu Data Factory varlıklarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="9b6fb-130">Bir ODBC veri deposundan verileri kopyalamak için kullanılan Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: ODBC veri verilerini depolamak için Azure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an ODBC data store, see [JSON example: Copy data from ODBC data store to Azure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="9b6fb-131">Aşağıdaki bölümler, Data Factory varlıklarını belirli ODBC veri deposuna tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="9b6fb-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to ODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="9b6fb-132">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="9b6fb-132">Linked service properties</span></span>
<span data-ttu-id="9b6fb-133">Aşağıdaki tabloda, JSON öğeleri için ODBC belirli açıklamasını bağlantılı hizmetinin sağlar.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-133">The following table provides description for JSON elements specific to ODBC linked service.</span></span>

| <span data-ttu-id="9b6fb-134">Özellik</span><span class="sxs-lookup"><span data-stu-id="9b6fb-134">Property</span></span> | <span data-ttu-id="9b6fb-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9b6fb-135">Description</span></span> | <span data-ttu-id="9b6fb-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9b6fb-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9b6fb-137">type</span><span class="sxs-lookup"><span data-stu-id="9b6fb-137">type</span></span> |<span data-ttu-id="9b6fb-138">Type özelliği ayarlanmalıdır: **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="9b6fb-138">The type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="9b6fb-139">Evet</span><span class="sxs-lookup"><span data-stu-id="9b6fb-139">Yes</span></span> |
| <span data-ttu-id="9b6fb-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="9b6fb-140">connectionString</span></span> |<span data-ttu-id="9b6fb-141">Bağlantı dizesi ve isteğe bağlı şifrelenmiş kimlik bilgileri olmayan erişim kimlik bilgileri bölümü.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-141">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="9b6fb-142">Aşağıdaki bölümlerde örneklere bakın.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-142">See examples in the following sections.</span></span> |<span data-ttu-id="9b6fb-143">Evet</span><span class="sxs-lookup"><span data-stu-id="9b6fb-143">Yes</span></span> |
| <span data-ttu-id="9b6fb-144">kimlik bilgisi</span><span class="sxs-lookup"><span data-stu-id="9b6fb-144">credential</span></span> |<span data-ttu-id="9b6fb-145">Sürücü özgü özellik değer biçiminde belirtilen bağlantı dizesi erişim kimlik bilgisi bölümü.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-145">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="9b6fb-146">Örnek: "Uid =<user ID>; PWD =<password>; RefreshToken =<secret refresh token>; ".</span><span class="sxs-lookup"><span data-stu-id="9b6fb-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="9b6fb-147">Hayır</span><span class="sxs-lookup"><span data-stu-id="9b6fb-147">No</span></span> |
| <span data-ttu-id="9b6fb-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="9b6fb-148">authenticationType</span></span> |<span data-ttu-id="9b6fb-149">ODBC veri deposuna bağlanmak için kullanılan kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-149">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="9b6fb-150">Olası değerler şunlardır: anonim ve temel.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="9b6fb-151">Evet</span><span class="sxs-lookup"><span data-stu-id="9b6fb-151">Yes</span></span> |
| <span data-ttu-id="9b6fb-152">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="9b6fb-152">username</span></span> |<span data-ttu-id="9b6fb-153">Temel kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="9b6fb-154">Hayır</span><span class="sxs-lookup"><span data-stu-id="9b6fb-154">No</span></span> |
| <span data-ttu-id="9b6fb-155">password</span><span class="sxs-lookup"><span data-stu-id="9b6fb-155">password</span></span> |<span data-ttu-id="9b6fb-156">Kullanıcı adı için belirtilen kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-156">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="9b6fb-157">Hayır</span><span class="sxs-lookup"><span data-stu-id="9b6fb-157">No</span></span> |
| <span data-ttu-id="9b6fb-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="9b6fb-158">gatewayName</span></span> |<span data-ttu-id="9b6fb-159">Data Factory hizmetinin ODBC veri deposuna bağlanmak için kullanması gereken ağ geçidinin adı.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-159">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="9b6fb-160">Evet</span><span class="sxs-lookup"><span data-stu-id="9b6fb-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="9b6fb-161">Temel kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="9b6fb-161">Using Basic authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="9b6fb-162">Temel kimlik doğrulaması ile şifrelenmiş kimlik bilgileri kullanma</span><span class="sxs-lookup"><span data-stu-id="9b6fb-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="9b6fb-163">Kullanarak kimlik bilgilerini şifrelemek [yeni AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (Azure PowerShell 1.0 sürümü) cmdlet'ini veya [yeni AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (Azure PowerShell 0,9 veya önceki sürüm).</span><span class="sxs-lookup"><span data-stu-id="9b6fb-163">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="9b6fb-164">Anonim kimlik doğrulamasını kullanma</span><span class="sxs-lookup"><span data-stu-id="9b6fb-164">Using Anonymous authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a><span data-ttu-id="9b6fb-165">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="9b6fb-165">Dataset properties</span></span>
<span data-ttu-id="9b6fb-166">Bölümler & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="9b6fb-167">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="9b6fb-168">**TypeProperties** bölüm veri kümesi her tür için farklıdır ve verilerin veri deposunda konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="9b6fb-169">TypeProperties bölüm türü veri kümesi için **RelationalTable** (ODBC veri kümesi içeren) aşağıdaki özelliklere sahip</span><span class="sxs-lookup"><span data-stu-id="9b6fb-169">The typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has the following properties</span></span>

| <span data-ttu-id="9b6fb-170">Özellik</span><span class="sxs-lookup"><span data-stu-id="9b6fb-170">Property</span></span> | <span data-ttu-id="9b6fb-171">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9b6fb-171">Description</span></span> | <span data-ttu-id="9b6fb-172">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9b6fb-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9b6fb-173">tableName</span><span class="sxs-lookup"><span data-stu-id="9b6fb-173">tableName</span></span> |<span data-ttu-id="9b6fb-174">ODBC veri deposundaki tablonun adı.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-174">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="9b6fb-175">Evet</span><span class="sxs-lookup"><span data-stu-id="9b6fb-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="9b6fb-176">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="9b6fb-176">Copy activity properties</span></span>
<span data-ttu-id="9b6fb-177">Bölümler & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz: [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-177">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="9b6fb-178">Ad, açıklama, giriş ve çıkış tabloları ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="9b6fb-179">Kullanılabilir özellikler **typeProperties** etkinlik bölümünü diğer yandan her etkinlik türü ile değişir.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-179">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="9b6fb-180">Kopya etkinliği için bunlar türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-180">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="9b6fb-181">Kopyalama etkinliğinde kaynak türü olduğunda **RelationalSource** (içeren ODBC), aşağıdaki özellikler typeProperties bölümünde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="9b6fb-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="9b6fb-182">Özellik</span><span class="sxs-lookup"><span data-stu-id="9b6fb-182">Property</span></span> | <span data-ttu-id="9b6fb-183">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9b6fb-183">Description</span></span> | <span data-ttu-id="9b6fb-184">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="9b6fb-184">Allowed values</span></span> | <span data-ttu-id="9b6fb-185">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9b6fb-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9b6fb-186">sorgu</span><span class="sxs-lookup"><span data-stu-id="9b6fb-186">query</span></span> |<span data-ttu-id="9b6fb-187">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-187">Use the custom query to read data.</span></span> |<span data-ttu-id="9b6fb-188">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-188">SQL query string.</span></span> <span data-ttu-id="9b6fb-189">Örneğin: seçin * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="9b6fb-190">Evet</span><span class="sxs-lookup"><span data-stu-id="9b6fb-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-to-azure-blob"></a><span data-ttu-id="9b6fb-191">JSON örnek: ODBC veri verilerini depolamak için Azure Blob</span><span class="sxs-lookup"><span data-stu-id="9b6fb-191">JSON example: Copy data from ODBC data store to Azure Blob</span></span>
<span data-ttu-id="9b6fb-192">Bu örnek kullanarak bir işlem hattı oluşturmak için kullanabileceğiniz JSON tanımları sağlar, [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9b6fb-192">This example provides JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="9b6fb-193">Bir Azure Blob depolama alanına bir ODBC kaynağından veri kopyalamak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-193">It shows how to copy data from an ODBC source to an Azure Blob Storage.</span></span> <span data-ttu-id="9b6fb-194">Ancak, veri herhangi belirtildiği havuzlarını kopyalanabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kopya etkinliği Azure Data Factory kullanarak.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-194">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="9b6fb-195">Örnek aşağıdaki data factory varlıklarını sahiptir:</span><span class="sxs-lookup"><span data-stu-id="9b6fb-195">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="9b6fb-196">Bağlı hizmet türü [OnPremisesOdbc](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9b6fb-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="9b6fb-197">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9b6fb-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="9b6fb-198">Bir giriş [dataset](data-factory-create-datasets.md) türü [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9b6fb-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="9b6fb-199">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9b6fb-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="9b6fb-200">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="9b6fb-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="9b6fb-201">Örnek veri sorgu sonucu bir ODBC veri deposundaki bir blobu saatte kopyalar.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-201">The sample copies data from a query result in an ODBC data store to a blob every hour.</span></span> <span data-ttu-id="9b6fb-202">Bu örnekler kullanılan JSON özellikleri örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-202">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="9b6fb-203">İlk adım olarak, veri yönetimi ağ geçidi kurun ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-203">As a first step, set up the data management gateway.</span></span> <span data-ttu-id="9b6fb-204">Yönergeler bulunan [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-204">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="9b6fb-205">**ODBC bağlantılı hizmeti** Bu örnek, temel kimlik doğrulaması kullanır.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-205">**ODBC linked service** This example uses the Basic authentication.</span></span> <span data-ttu-id="9b6fb-206">Bkz: [ODBC bağlantılı hizmeti](#linked-service-properties) bölümü için farklı tür kimlik doğrulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="9b6fb-207">**Azure Storage bağlı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="9b6fb-207">**Azure Storage linked service**</span></span>

```json
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

<span data-ttu-id="9b6fb-208">**ODBC girdi veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="9b6fb-208">**ODBC input dataset**</span></span>

<span data-ttu-id="9b6fb-209">Örnek bir ODBC veritabanında bir tablo "MyTable" oluşturdunuz ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-209">The sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="9b6fb-210">"Dış" ayarı: "true" bildirir Data Factory hizmetinin veri kümesi data factory dış ve veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-210">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

<span data-ttu-id="9b6fb-211">**Azure Blob dataset çıktı**</span><span class="sxs-lookup"><span data-stu-id="9b6fb-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="9b6fb-212">Veri her saat yeni bir bloba yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="9b6fb-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="9b6fb-213">Blob klasör yolu dinamik işlenmekte olan dilim başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="9b6fb-214">Klasör yolu yıl, ay, gün ve saat bölümleri başlangıç saatini kullanır.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


<span data-ttu-id="9b6fb-215">**ODBC kaynak (RelationalSource) ve Blob havuz (BlobSink) sahip işlem hattı kopyalama etkinliği**</span><span class="sxs-lookup"><span data-stu-id="9b6fb-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="9b6fb-216">Ardışık Düzen bu girdi ve çıktı veri kümeleri kullanmak üzere yapılandırıldığı ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-216">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="9b6fb-217">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **RelationalSource** ve **havuz** türü ayarlanmış **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="9b6fb-218">SQL sorgusu için belirtilen **sorgu** özelliği veri kopyalamak için son bir saat içindeki seçer.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="9b6fb-219">Tür eşlemesi için ODBC</span><span class="sxs-lookup"><span data-stu-id="9b6fb-219">Type mapping for ODBC</span></span>
<span data-ttu-id="9b6fb-220">Bölümünde belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği, aşağıdaki iki aşamalı yaklaşımı türleriyle havuz için kaynak türünden otomatik tür dönüşümleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="9b6fb-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="9b6fb-221">Yerel kaynak türlerinden .NET türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="9b6fb-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="9b6fb-222">.NET türünden yerel havuz türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="9b6fb-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="9b6fb-223">ODBC veri depolarına verilerin taşınması, ODBC veri türleri .NET türlerine bölümünde belirtildiği gibi eşlenir [ODBC veri türü eşlemeleri](https://msdn.microsoft.com/library/cc668763.aspx) konu.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-223">When moving data from ODBC data stores, ODBC data types are mapped to .NET types as mentioned in the [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="9b6fb-224">Kaynak havuzu sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="9b6fb-224">Map source to sink columns</span></span>
<span data-ttu-id="9b6fb-225">Havuz dataset sütunlara kaynak kümesindeki eşleme sütunları hakkında bilgi edinmek için [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="9b6fb-225">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="9b6fb-226">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="9b6fb-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="9b6fb-227">İlişkisel veri kopyalama verileri depoladığında, Yinelenebilirlik istenmeyen sonuçları önlemek için göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-227">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="9b6fb-228">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="9b6fb-229">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="9b6fb-230">Bir dilim iki yolla yeniden çalıştırıldığında, aynı veri dilimi çalıştırmak kaç kez geçtiğinden bağımsız okuduğunuzdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-230">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="9b6fb-231">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="9b6fb-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="9b6fb-232">GE Historian deposu</span><span class="sxs-lookup"><span data-stu-id="9b6fb-232">GE Historian store</span></span>
<span data-ttu-id="9b6fb-233">Bağlantı için bir ODBC bağlı hizmeti oluşturma bir [GE Proficy Historian (şimdi GE Historian)](http://www.geautomation.com/products/proficy-historian) aşağıdaki örnekte gösterildiği gibi verileri depolamak için bir Azure data factory:</span><span class="sxs-lookup"><span data-stu-id="9b6fb-233">You create an ODBC linked service to link a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store to an Azure data factory as shown in the following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of the GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="9b6fb-234">Veri Yönetimi ağ geçidi bir şirket içi makineye yükleyin ve ağ geçidi portal ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-234">Install Data Management Gateway on an on-premises machine and register the gateway with the portal.</span></span> <span data-ttu-id="9b6fb-235">Şirket içi bilgisayarınıza yüklü olan ağ geçidini GE Historian için ODBC sürücüsü GE Historian veri deposuna bağlanmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-235">The gateway installed on your on-premises computer uses the ODBC driver for GE Historian to connect to the GE Historian data store.</span></span> <span data-ttu-id="9b6fb-236">Bu nedenle, ağ geçidi makinede zaten yüklü değilse sürücüyü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-236">Therefore, install the driver if it is not already installed on the gateway machine.</span></span> <span data-ttu-id="9b6fb-237">Bkz: [bağlantıyı etkinleştirme](#enabling-connectivity) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="9b6fb-238">Veri Fabrikası çözüm GE Historian deposunda kullanmadan önce ağ geçidi bir sonraki bölümde yönergeleri kullanarak veri depolama alanı bağlanıp bağlanamadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-238">Before you use the GE Historian store in a Data Factory solution, verify whether the gateway can connect to the data store using instructions in the next section.</span></span>

<span data-ttu-id="9b6fb-239">ODBC veri kullanarak makale ayrıntılı bir genel bakış için en başından bir kopyalama işleminde kaynak veri depoları olarak depolar okuyun.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-239">Read the article from the beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="9b6fb-240">Bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="9b6fb-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="9b6fb-241">Bağlantı sorunlarını gidermek için kullanmak **tanılama** sekmesinde **veri yönetimi ağ geçidi Yapılandırma Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-241">To troubleshoot connection issues, use the **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="9b6fb-242">Başlatma **veri yönetimi ağ geçidi Yapılandırma Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="9b6fb-243">İçin "C:\Program Files\Microsoft veri yönetimi Gateway\1.0\Shared\ConfigManager.exe" doğrudan (veya) arama ya da çalıştırabilirsiniz **ağ geçidi** bağlantı bulmak için **Microsoft Veri Yönetimi ağ geçidi** aşağıdaki görüntüde gösterildiği gibi uygulama.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** to find a link to **Microsoft Data Management Gateway** application as shown in the following image.</span></span>

    ![Arama ağ geçidi](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="9b6fb-245">Geçiş **tanılama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-245">Switch to the **Diagnostics** tab.</span></span>

    ![Ağ geçidi tanılama](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="9b6fb-247">Seçin **türü** (bağlantılı hizmeti) verilerini depolar.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-247">Select the **type** of data store (linked service).</span></span>
4. <span data-ttu-id="9b6fb-248">Belirtin **kimlik doğrulaması** ve girin **kimlik bilgileri** (veya) girin **bağlantı dizesi** veri deposuna bağlanmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used to connect to the data store.</span></span>
5. <span data-ttu-id="9b6fb-249">Tıklatın **Bağlantıyı Sına** veri deposu test edin.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-249">Click **Test connection** to test the connection to the data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="9b6fb-250">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="9b6fb-250">Performance and Tuning</span></span>
<span data-ttu-id="9b6fb-251">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve onu en iyi duruma getirmek için çeşitli yollar etkisi performansını anahtar Etkenler hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="9b6fb-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
