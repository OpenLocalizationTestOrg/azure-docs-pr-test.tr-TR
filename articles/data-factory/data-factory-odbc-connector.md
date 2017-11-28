---
title: "ODBC veri depolarına aaaMove verilerden | Microsoft Docs"
description: "Azure Data Factory kullanarak ODBC veri toomove verileri nasıl depolar hakkında bilgi edinin."
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
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="fdcb1-103">Azure Data Factory kullanarak veri öğesinden ODBC veri depolarını taşıma</span><span class="sxs-lookup"><span data-stu-id="fdcb1-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="fdcb1-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove verileri bir şirket içi ODBC veri depolamak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises ODBC data store.</span></span> <span data-ttu-id="fdcb1-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="fdcb1-106">Bir ODBC veri deposu desteklenen tooany havuz veri deposundan verileri kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-106">You can copy data from an ODBC data store tooany supported sink data store.</span></span> <span data-ttu-id="fdcb1-107">Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="fdcb1-108">Veri Fabrikası şu anda bir ODBC veri verilerden tooother veri depolarına depolamak taşıma yalnızca, ancak diğer veri depoları tooan ODBC veri deposundan veri taşıma değil destekler.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-108">Data factory currently supports only moving data from an ODBC data store tooother data stores, but not for moving data from other data stores tooan ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="fdcb1-109">Bağlantıyı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="fdcb1-109">Enabling connectivity</span></span>
<span data-ttu-id="fdcb1-110">Data Factory Hizmeti'ne hello veri yönetimi ağ geçidi kullanarak bağlanan tooon içi ODBC kaynakları destekler.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-110">Data Factory service supports connecting tooon-premises ODBC sources using hello Data Management Gateway.</span></span> <span data-ttu-id="fdcb1-111">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale toolearn veri yönetimi ağ geçidi ve hello ağ geçidi kurun ayarlama hakkında adım adım yönergeleri hakkında.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="fdcb1-112">Bir Azure Iaas sanal barındırılan olsa bile hello ağ geçidi tooconnect tooan ODBC veri deposunu kullan.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-112">Use hello gateway tooconnect tooan ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="fdcb1-113">Merhaba ağ geçidi içi aynı makine veya hello ODBC veri deposu olarak Azure VM hello hello yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-113">You can install hello gateway on hello same on-premises machine or hello Azure VM as hello ODBC data store.</span></span> <span data-ttu-id="fdcb1-114">Ancak, bir ayrı makine/Azure Iaas VM hello ağ geçidi yüklemenizi öneririz tooavoid kaynak çekişmesini ve daha iyi performans için.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-114">However, we recommend that you install hello gateway on a separate machine/Azure IaaS VM tooavoid resource contention and for better performance.</span></span> <span data-ttu-id="fdcb1-115">Merhaba ağ geçidi ayrı bir makineye yüklediğinizde hello makine hello ODBC veri deposu ile mümkün tooaccess hello makine olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-115">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello ODBC data store.</span></span>

<span data-ttu-id="fdcb1-116">Veri Yönetimi ağ geçidi Hello dışında ayrıca tooinstall hello ODBC sürücüsü hello veri deposu hello gateway makinesinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-116">Apart from hello Data Management Gateway, you also need tooinstall hello ODBC driver for hello data store on hello gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="fdcb1-117">Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="fdcb1-118">Başlarken</span><span class="sxs-lookup"><span data-stu-id="fdcb1-118">Getting started</span></span>
<span data-ttu-id="fdcb1-119">Farklı araçlar/API'lerini kullanarak bir ODBC veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="fdcb1-120">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="fdcb1-121">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="fdcb1-122">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu **, **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="fdcb1-123">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="fdcb1-124">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fdcb1-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="fdcb1-125">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="fdcb1-126">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="fdcb1-127">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="fdcb1-128">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="fdcb1-129">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="fdcb1-130">Bir ODBC veri deposundaki kullanılan toocopy verileri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: ODBC veri verilerini depolamak tooAzure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an ODBC data store, see [JSON example: Copy data from ODBC data store tooAzure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="fdcb1-131">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooODBC veri deposu olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="fdcb1-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="fdcb1-132">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="fdcb1-132">Linked service properties</span></span>
<span data-ttu-id="fdcb1-133">Aşağıdaki tablonun hello JSON öğeleri belirli tooODBC bağlantılı hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-133">hello following table provides description for JSON elements specific tooODBC linked service.</span></span>

| <span data-ttu-id="fdcb1-134">Özellik</span><span class="sxs-lookup"><span data-stu-id="fdcb1-134">Property</span></span> | <span data-ttu-id="fdcb1-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdcb1-135">Description</span></span> | <span data-ttu-id="fdcb1-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fdcb1-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fdcb1-137">type</span><span class="sxs-lookup"><span data-stu-id="fdcb1-137">type</span></span> |<span data-ttu-id="fdcb1-138">Merhaba type özelliği ayarlanmalıdır: **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="fdcb1-138">hello type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="fdcb1-139">Evet</span><span class="sxs-lookup"><span data-stu-id="fdcb1-139">Yes</span></span> |
| <span data-ttu-id="fdcb1-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="fdcb1-140">connectionString</span></span> |<span data-ttu-id="fdcb1-141">Merhaba olmayan erişim kimlik bilgisi kısmı hello bağlantı dizesini ve isteğe bağlı bir kimlik bilgisi şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-141">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="fdcb1-142">Aşağıdaki bölümlerde hello örneklere bakın.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-142">See examples in hello following sections.</span></span> |<span data-ttu-id="fdcb1-143">Evet</span><span class="sxs-lookup"><span data-stu-id="fdcb1-143">Yes</span></span> |
| <span data-ttu-id="fdcb1-144">kimlik bilgisi</span><span class="sxs-lookup"><span data-stu-id="fdcb1-144">credential</span></span> |<span data-ttu-id="fdcb1-145">Merhaba erişim kimlik bilgisi bölümü sürücüye özgü özellik değer biçiminde belirtilen hello bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-145">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="fdcb1-146">Örnek: "Uid =<user ID>; PWD =<password>; RefreshToken =<secret refresh token>; ".</span><span class="sxs-lookup"><span data-stu-id="fdcb1-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="fdcb1-147">Hayır</span><span class="sxs-lookup"><span data-stu-id="fdcb1-147">No</span></span> |
| <span data-ttu-id="fdcb1-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="fdcb1-148">authenticationType</span></span> |<span data-ttu-id="fdcb1-149">Kimlik doğrulama türü tooconnect toohello ODBC veri deposu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-149">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="fdcb1-150">Olası değerler şunlardır: anonim ve temel.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="fdcb1-151">Evet</span><span class="sxs-lookup"><span data-stu-id="fdcb1-151">Yes</span></span> |
| <span data-ttu-id="fdcb1-152">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="fdcb1-152">username</span></span> |<span data-ttu-id="fdcb1-153">Temel kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="fdcb1-154">Hayır</span><span class="sxs-lookup"><span data-stu-id="fdcb1-154">No</span></span> |
| <span data-ttu-id="fdcb1-155">password</span><span class="sxs-lookup"><span data-stu-id="fdcb1-155">password</span></span> |<span data-ttu-id="fdcb1-156">Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-156">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="fdcb1-157">Hayır</span><span class="sxs-lookup"><span data-stu-id="fdcb1-157">No</span></span> |
| <span data-ttu-id="fdcb1-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="fdcb1-158">gatewayName</span></span> |<span data-ttu-id="fdcb1-159">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello ODBC veri deposu kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="fdcb1-160">Evet</span><span class="sxs-lookup"><span data-stu-id="fdcb1-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="fdcb1-161">Temel kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="fdcb1-161">Using Basic authentication</span></span>

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
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="fdcb1-162">Temel kimlik doğrulaması ile şifrelenmiş kimlik bilgileri kullanma</span><span class="sxs-lookup"><span data-stu-id="fdcb1-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="fdcb1-163">Merhaba kimlik hello kullanarak şifreleyebilirsiniz [yeni AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (Azure PowerShell 1.0 sürümü) cmdlet'ini veya [yeni AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 veya önceki bir sürümü hello Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="fdcb1-163">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

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

### <a name="using-anonymous-authentication"></a><span data-ttu-id="fdcb1-164">Anonim kimlik doğrulamasını kullanma</span><span class="sxs-lookup"><span data-stu-id="fdcb1-164">Using Anonymous authentication</span></span>

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


## <a name="dataset-properties"></a><span data-ttu-id="fdcb1-165">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="fdcb1-165">Dataset properties</span></span>
<span data-ttu-id="fdcb1-166">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="fdcb1-167">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="fdcb1-168">Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="fdcb1-169">Merhaba typeProperties bölüm türü veri kümesi için **RelationalTable** hello aşağıdaki özelliklere sahip (ODBC veri kümesi içerir)</span><span class="sxs-lookup"><span data-stu-id="fdcb1-169">hello typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has hello following properties</span></span>

| <span data-ttu-id="fdcb1-170">Özellik</span><span class="sxs-lookup"><span data-stu-id="fdcb1-170">Property</span></span> | <span data-ttu-id="fdcb1-171">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdcb1-171">Description</span></span> | <span data-ttu-id="fdcb1-172">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fdcb1-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fdcb1-173">tableName</span><span class="sxs-lookup"><span data-stu-id="fdcb1-173">tableName</span></span> |<span data-ttu-id="fdcb1-174">Merhaba ODBC veri deposundaki Merhaba tablonun adı.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-174">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="fdcb1-175">Evet</span><span class="sxs-lookup"><span data-stu-id="fdcb1-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="fdcb1-176">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="fdcb1-176">Copy activity properties</span></span>
<span data-ttu-id="fdcb1-177">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-177">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="fdcb1-178">Ad, açıklama, giriş ve çıkış tabloları ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="fdcb1-179">Hello kullanılabilen özellikleri **typeProperties** bölüm diğer yandan hello hello faaliyete, her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-179">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="fdcb1-180">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-180">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="fdcb1-181">Kopyalama etkinliğinde kaynak türü olduğunda **RelationalSource** (içeren ODBC), aşağıdaki özelliklere hello typeProperties bölümünde bulunur:</span><span class="sxs-lookup"><span data-stu-id="fdcb1-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="fdcb1-182">Özellik</span><span class="sxs-lookup"><span data-stu-id="fdcb1-182">Property</span></span> | <span data-ttu-id="fdcb1-183">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdcb1-183">Description</span></span> | <span data-ttu-id="fdcb1-184">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="fdcb1-184">Allowed values</span></span> | <span data-ttu-id="fdcb1-185">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fdcb1-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fdcb1-186">sorgu</span><span class="sxs-lookup"><span data-stu-id="fdcb1-186">query</span></span> |<span data-ttu-id="fdcb1-187">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-187">Use hello custom query tooread data.</span></span> |<span data-ttu-id="fdcb1-188">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-188">SQL query string.</span></span> <span data-ttu-id="fdcb1-189">Örneğin: seçin * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="fdcb1-190">Evet</span><span class="sxs-lookup"><span data-stu-id="fdcb1-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a><span data-ttu-id="fdcb1-191">JSON örnek: ODBC veri verilerini depolamak tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="fdcb1-191">JSON example: Copy data from ODBC data store tooAzure Blob</span></span>
<span data-ttu-id="fdcb1-192">Bu örnek JSON tanımları sağlar, toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fdcb1-192">This example provides JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="fdcb1-193">Bunu nasıl tooan Azure Blob Storage toocopy bir ODBC veri kaynağı gösterir.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-193">It shows how toocopy data from an ODBC source tooan Azure Blob Storage.</span></span> <span data-ttu-id="fdcb1-194">Ancak, veri belirtildiği hello havuzlarını, kopyalanan tooany olabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-194">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="fdcb1-195">Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="fdcb1-195">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="fdcb1-196">Bağlı hizmet türü [OnPremisesOdbc](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fdcb1-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="fdcb1-197">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fdcb1-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="fdcb1-198">Bir giriş [dataset](data-factory-create-datasets.md) türü [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fdcb1-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="fdcb1-199">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fdcb1-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="fdcb1-200">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="fdcb1-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="fdcb1-201">Merhaba örnek verileri bir ODBC veri deposu tooa blob bir sorgu sonucunda her saat kopyalar.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-201">hello sample copies data from a query result in an ODBC data store tooa blob every hour.</span></span> <span data-ttu-id="fdcb1-202">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-202">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="fdcb1-203">İlk adım olarak, hello veri yönetimi ağ geçidi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-203">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="fdcb1-204">Merhaba yönergelerdir hello [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-204">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="fdcb1-205">**ODBC bağlantılı hizmeti** kullandığı hello temel kimlik doğrulaması Bu örnek.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-205">**ODBC linked service** This example uses hello Basic authentication.</span></span> <span data-ttu-id="fdcb1-206">Bkz: [ODBC bağlantılı hizmeti](#linked-service-properties) bölümü için farklı tür kimlik doğrulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="fdcb1-207">**Azure Storage bağlı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="fdcb1-207">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="fdcb1-208">**ODBC girdi veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="fdcb1-208">**ODBC input dataset**</span></span>

<span data-ttu-id="fdcb1-209">Merhaba örnek bir ODBC veritabanında bir tablo "MyTable" oluşturdunuz ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-209">hello sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="fdcb1-210">"Dış" ayarı: "true" bildirir hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-210">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="fdcb1-211">**Azure Blob dataset çıktı**</span><span class="sxs-lookup"><span data-stu-id="fdcb1-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="fdcb1-212">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="fdcb1-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="fdcb1-213">hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="fdcb1-214">Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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


<span data-ttu-id="fdcb1-215">**ODBC kaynak (RelationalSource) ve Blob havuz (BlobSink) sahip işlem hattı kopyalama etkinliği**</span><span class="sxs-lookup"><span data-stu-id="fdcb1-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="fdcb1-216">Merhaba ardışık düzen içeren bir kopyalama etkinliği, yapılandırılmış toouse bu girdi ve çıktı veri kümeleri ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-216">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="fdcb1-217">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**RelationalSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="fdcb1-218">Merhaba belirtilen hello SQL sorgusu **sorgu** özelliği saat toocopy geçmiş hello hello veri seçer.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="fdcb1-219">Tür eşlemesi için ODBC</span><span class="sxs-lookup"><span data-stu-id="fdcb1-219">Type mapping for ODBC</span></span>
<span data-ttu-id="fdcb1-220">Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri iki aşamalı bir yaklaşım aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="fdcb1-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="fdcb1-221">Yerel kaynak türleri too.NET türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="fdcb1-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="fdcb1-222">.NET türü toonative havuz türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="fdcb1-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="fdcb1-223">ODBC veri depolarına verilerin taşınması, ODBC veri türleri eşlenen too.NET hello belirtildiği gibi türleridir [ODBC veri türü eşlemeleri](https://msdn.microsoft.com/library/cc668763.aspx) konu.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-223">When moving data from ODBC data stores, ODBC data types are mapped too.NET types as mentioned in hello [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="fdcb1-224">Kaynak toosink sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="fdcb1-224">Map source toosink columns</span></span>
<span data-ttu-id="fdcb1-225">Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="fdcb1-225">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="fdcb1-226">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="fdcb1-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="fdcb1-227">İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-227">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="fdcb1-228">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="fdcb1-229">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="fdcb1-230">Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-230">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="fdcb1-231">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="fdcb1-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="fdcb1-232">GE Historian deposu</span><span class="sxs-lookup"><span data-stu-id="fdcb1-232">GE Historian store</span></span>
<span data-ttu-id="fdcb1-233">Bir ODBC bağlantılı hizmet toolink oluşturduğunuz bir [GE Proficy Historian (şimdi GE Historian)](http://www.geautomation.com/products/proficy-historian) hello aşağıdaki örnekte gösterildiği gibi verileri depolamak tooan Azure veri fabrikası:</span><span class="sxs-lookup"><span data-stu-id="fdcb1-233">You create an ODBC linked service toolink a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store tooan Azure data factory as shown in hello following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="fdcb1-234">Bir şirket içi veri yönetimi ağ geçidi yükleyin ve hello portalıyla hello ağ geçidini kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-234">Install Data Management Gateway on an on-premises machine and register hello gateway with hello portal.</span></span> <span data-ttu-id="fdcb1-235">Şirket içi bilgisayarınıza yüklü hello ağ geçidi hello ODBC sürücüsü GE Historian tooconnect toohello GE Historian veri deposu kullanır.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-235">hello gateway installed on your on-premises computer uses hello ODBC driver for GE Historian tooconnect toohello GE Historian data store.</span></span> <span data-ttu-id="fdcb1-236">Merhaba ağ geçidi makinede zaten yüklü değilse, bu nedenle, hello sürücüsünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-236">Therefore, install hello driver if it is not already installed on hello gateway machine.</span></span> <span data-ttu-id="fdcb1-237">Bkz: [bağlantıyı etkinleştirme](#enabling-connectivity) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="fdcb1-238">GE Historian depolamak bir veri fabrikası çözümde hello kullanmadan önce hello ağ geçidi toohello veri deposu hello sonraki bölümde yönergeleri kullanarak bağlandığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-238">Before you use hello GE Historian store in a Data Factory solution, verify whether hello gateway can connect toohello data store using instructions in hello next section.</span></span>

<span data-ttu-id="fdcb1-239">ODBC veri kullanımının hello makale okuma ayrıntılı bir genel bakış için hello başından bir kopyalama işleminde kaynak veri depoları olarak depolar.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-239">Read hello article from hello beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="fdcb1-240">Bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="fdcb1-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="fdcb1-241">tootroubleshoot bağlantı sorunlarını kullanmak hello **tanılama** sekmesinde **veri yönetimi ağ geçidi Yapılandırma Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-241">tootroubleshoot connection issues, use hello **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="fdcb1-242">Başlatma **veri yönetimi ağ geçidi Yapılandırma Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="fdcb1-243">İçin "C:\Program Files\Microsoft veri yönetimi Gateway\1.0\Shared\ConfigManager.exe" doğrudan (veya) arama ya da çalıştırabilirsiniz **ağ geçidi** toofind bağlantı çok**Microsoft Veri Yönetimi ağ geçidi** Görüntü aşağıdaki hello gösterildiği gibi uygulama.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** toofind a link too**Microsoft Data Management Gateway** application as shown in hello following image.</span></span>

    ![Arama ağ geçidi](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="fdcb1-245">Geçiş toohello **tanılama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-245">Switch toohello **Diagnostics** tab.</span></span>

    ![Ağ geçidi tanılama](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="fdcb1-247">Select hello **türü** (bağlantılı hizmeti) verilerini depolar.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-247">Select hello **type** of data store (linked service).</span></span>
4. <span data-ttu-id="fdcb1-248">Belirtin **kimlik doğrulaması** ve girin **kimlik bilgileri** (veya) girin **bağlantı dizesi** , kullanılan tooconnect toohello veri deposudur.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used tooconnect toohello data store.</span></span>
5. <span data-ttu-id="fdcb1-249">Tıklatın **Bağlantıyı Sına** tootest hello bağlantı toohello veri deposu.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-249">Click **Test connection** tootest hello connection toohello data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="fdcb1-250">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="fdcb1-250">Performance and Tuning</span></span>
<span data-ttu-id="fdcb1-251">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="fdcb1-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
