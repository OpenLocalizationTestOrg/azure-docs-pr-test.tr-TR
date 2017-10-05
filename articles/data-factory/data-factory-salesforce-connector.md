---
title: "Veri Fabrikası kullanarak Salesforce veri taşıma | Microsoft Docs"
description: "Azure Data Factory kullanarak Salesforce veri taşıma hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 9390b992bce2dede750c3fc55b7783a6b0db678f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="a60ff-103">Azure Data Factory kullanarak Salesforce taşıma verileri</span><span class="sxs-lookup"><span data-stu-id="a60ff-103">Move data from Salesforce by using Azure Data Factory</span></span>
<span data-ttu-id="a60ff-104">Bu makalede kopyalama etkinliği bir Azure data factory havuz sütunu altında listelenen herhangi bir veri deposuna Salesforce verileri kopyalamak için nasıl kullanacağınızı özetlenmektedir [desteklenen kaynakları ve havuzlarını](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="a60ff-104">This article outlines how you can use Copy Activity in an Azure data factory to copy data from Salesforce to any data store that is listed under the Sink column in the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="a60ff-105">Bu makalede derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) desteklenen veri deposu birleşimleri kopyalama etkinliği ile veri taşıma için genel bir bakış sunan makalesi.</span><span class="sxs-lookup"><span data-stu-id="a60ff-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="a60ff-106">Azure Data Factory şu anda yalnızca taşıma için Salesforce verilerden destekler [havuz veri depolarına desteklenen](data-factory-data-movement-activities.md#supported-data-stores-and-formats), ancak verileri diğer veriler taşıma desteklemediği için Salesforce depolar.</span><span class="sxs-lookup"><span data-stu-id="a60ff-106">Azure Data Factory currently supports only moving data from Salesforce to [supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores to Salesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="a60ff-107">Desteklenen sürümler</span><span class="sxs-lookup"><span data-stu-id="a60ff-107">Supported versions</span></span>
<span data-ttu-id="a60ff-108">Bu bağlayıcı Salesforce aşağıdaki sürümlerini destekler: Geliştirici sürümü, Professional Edition, Enterprise Edition veya sınırsız sürümü.</span><span class="sxs-lookup"><span data-stu-id="a60ff-108">This connector supports the following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="a60ff-109">Ve Salesforce üretim, korumalı alan ve özel etki alanı kopyalama destekler.</span><span class="sxs-lookup"><span data-stu-id="a60ff-109">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a60ff-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a60ff-110">Prerequisites</span></span>
* <span data-ttu-id="a60ff-111">API izni etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a60ff-111">API permission must be enabled.</span></span> <span data-ttu-id="a60ff-112">Bkz: [nasıl Salesforce API erişim izni kümesi tarafından etkinleştirebilirim?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span><span class="sxs-lookup"><span data-stu-id="a60ff-112">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="a60ff-113">Şirket içi veri depolarına Salesforce verileri kopyalamak için en az olmalıdır veri yönetimi ağ geçidi şirket içi ortamınızda yüklü 2.0.</span><span class="sxs-lookup"><span data-stu-id="a60ff-113">To copy data from Salesforce to on-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="a60ff-114">Salesforce istek sınırları</span><span class="sxs-lookup"><span data-stu-id="a60ff-114">Salesforce request limits</span></span>
<span data-ttu-id="a60ff-115">Salesforce toplam API istekleri ve eşzamanlı API istekleri için sınırları vardır.</span><span class="sxs-lookup"><span data-stu-id="a60ff-115">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="a60ff-116">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="a60ff-116">Note the following points:</span></span>

- <span data-ttu-id="a60ff-117">Eşzamanlı istek sayısı sınırı aşarsa, azaltma gerçekleşir ve rastgele hatalara görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a60ff-117">If the number of concurrent requests exceeds the limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="a60ff-118">Toplam istek sayısı sınırı aşarsa, 24 saat Salesforce hesap engellenir.</span><span class="sxs-lookup"><span data-stu-id="a60ff-118">If the total number of requests exceeds the limit, the Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="a60ff-119">Ayrıca, her iki senaryoda "REQUEST_LIMIT_EXCEEDED" hata iletisi.</span><span class="sxs-lookup"><span data-stu-id="a60ff-119">You might also receive the “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="a60ff-120">"API istek sınırları" bölümüne bakın [Salesforce Geliştirici sınırları](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="a60ff-120">See the "API Request Limits" section in the [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a60ff-121">Başlarken</span><span class="sxs-lookup"><span data-stu-id="a60ff-121">Getting started</span></span>
<span data-ttu-id="a60ff-122">Farklı araçlar/API'lerini kullanarak Salesforce verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a60ff-122">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="a60ff-123">Bir işlem hattı oluşturmak için en kolay yolu kullanmaktır **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="a60ff-123">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="a60ff-124">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) veri kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="a60ff-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="a60ff-125">Bir işlem hattı oluşturmak için aşağıdaki araçları kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu**, **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="a60ff-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a60ff-126">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="a60ff-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="a60ff-127">Araçlar ya da API'leri kullanıp bir havuz veri deposu için bir kaynak veri deposundan verileri taşır bir ardışık düzen oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="a60ff-127">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="a60ff-128">Oluşturma **bağlantılı Hizmetleri** girdi ve çıktı verilerini bağlamak için veri fabrikanıza depolar.</span><span class="sxs-lookup"><span data-stu-id="a60ff-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="a60ff-129">Oluşturma **veri kümeleri** kopyalama işlemi için girdi ve çıktı verilerini temsil etmek için.</span><span class="sxs-lookup"><span data-stu-id="a60ff-129">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="a60ff-130">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="a60ff-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="a60ff-131">Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a60ff-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="a60ff-132">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, JSON biçimini kullanarak bu Data Factory varlıklarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="a60ff-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="a60ff-133">Salesforce verileri kopyalamak için kullanılan Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: veri kopyalama Salesforce Azure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="a60ff-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from Salesforce, see [JSON example: Copy data from Salesforce to Azure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="a60ff-134">Aşağıdaki bölümler, belirli Data Factory varlıklarını Salesforce tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="a60ff-134">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Salesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="a60ff-135">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="a60ff-135">Linked service properties</span></span>
<span data-ttu-id="a60ff-136">Aşağıdaki tabloda Salesforce bağlantılı hizmete özgü JSON öğeleri için açıklamalar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a60ff-136">The following table provides descriptions for JSON elements that are specific to the Salesforce linked service.</span></span>

| <span data-ttu-id="a60ff-137">Özellik</span><span class="sxs-lookup"><span data-stu-id="a60ff-137">Property</span></span> | <span data-ttu-id="a60ff-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a60ff-138">Description</span></span> | <span data-ttu-id="a60ff-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a60ff-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a60ff-140">type</span><span class="sxs-lookup"><span data-stu-id="a60ff-140">type</span></span> |<span data-ttu-id="a60ff-141">Type özelliği ayarlanmalıdır: **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="a60ff-141">The type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="a60ff-142">Evet</span><span class="sxs-lookup"><span data-stu-id="a60ff-142">Yes</span></span> |
| <span data-ttu-id="a60ff-143">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="a60ff-143">environmentUrl</span></span> | <span data-ttu-id="a60ff-144">URL, Salesforce örneği belirtin.</span><span class="sxs-lookup"><span data-stu-id="a60ff-144">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="a60ff-145">-Varsayılan değer "https://login.salesforce.com" dir.</span><span class="sxs-lookup"><span data-stu-id="a60ff-145">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="a60ff-146">Korumalı alan veri kopyalamak için "https://test.salesforce.com" belirtin.</span><span class="sxs-lookup"><span data-stu-id="a60ff-146">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="a60ff-147">Özel etki alanından veri kopyalamak için örneğin, "https://[domain].my.salesforce.com" belirtin.</span><span class="sxs-lookup"><span data-stu-id="a60ff-147">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="a60ff-148">Hayır</span><span class="sxs-lookup"><span data-stu-id="a60ff-148">No</span></span> |
| <span data-ttu-id="a60ff-149">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="a60ff-149">username</span></span> |<span data-ttu-id="a60ff-150">Kullanıcı hesabı için bir kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="a60ff-150">Specify a user name for the user account.</span></span> |<span data-ttu-id="a60ff-151">Evet</span><span class="sxs-lookup"><span data-stu-id="a60ff-151">Yes</span></span> |
| <span data-ttu-id="a60ff-152">password</span><span class="sxs-lookup"><span data-stu-id="a60ff-152">password</span></span> |<span data-ttu-id="a60ff-153">Kullanıcı hesabı için bir parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="a60ff-153">Specify a password for the user account.</span></span> |<span data-ttu-id="a60ff-154">Evet</span><span class="sxs-lookup"><span data-stu-id="a60ff-154">Yes</span></span> |
| <span data-ttu-id="a60ff-155">securityToken</span><span class="sxs-lookup"><span data-stu-id="a60ff-155">securityToken</span></span> |<span data-ttu-id="a60ff-156">Kullanıcı hesabı için bir güvenlik belirteci belirtin.</span><span class="sxs-lookup"><span data-stu-id="a60ff-156">Specify a security token for the user account.</span></span> <span data-ttu-id="a60ff-157">Bkz: [güvenlik belirteci alma getirin](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) bir güvenlik belirteci sıfırlama/get ilgili yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="a60ff-157">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="a60ff-158">Güvenlik belirteçleri hakkında genel bilgi edinmek için [güvenlik ve API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="a60ff-158">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="a60ff-159">Evet</span><span class="sxs-lookup"><span data-stu-id="a60ff-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="a60ff-160">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="a60ff-160">Dataset properties</span></span>
<span data-ttu-id="a60ff-161">Bölümleri ve veri kümelerini tanımlamak için kullanılabilir olan özellikleri tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="a60ff-161">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a60ff-162">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri kümesi türleri için (Azure SQL, Azure blob, Azure tablo ve benzeri) benzer.</span><span class="sxs-lookup"><span data-stu-id="a60ff-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="a60ff-163">**TypeProperties** bölüm veri kümesi her tür için farklıdır ve verilerin veri deposunda konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a60ff-163">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="a60ff-164">TypeProperties bölüm türü veri kümesi için **RelationalTable** aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="a60ff-164">The typeProperties section for a dataset of the type **RelationalTable** has the following properties:</span></span>

| <span data-ttu-id="a60ff-165">Özellik</span><span class="sxs-lookup"><span data-stu-id="a60ff-165">Property</span></span> | <span data-ttu-id="a60ff-166">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a60ff-166">Description</span></span> | <span data-ttu-id="a60ff-167">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a60ff-167">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a60ff-168">tableName</span><span class="sxs-lookup"><span data-stu-id="a60ff-168">tableName</span></span> |<span data-ttu-id="a60ff-169">Salesforce tablo adı.</span><span class="sxs-lookup"><span data-stu-id="a60ff-169">Name of the table in Salesforce.</span></span> |<span data-ttu-id="a60ff-170">Hayır (varsa bir **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="a60ff-170">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="a60ff-171">API adı "__c" bölümü için herhangi bir özel nesne gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a60ff-171">The "__c" part of the API Name is needed for any custom object.</span></span>

![Veri Fabrikası - Salesforce bağlantı - API adı](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="a60ff-173">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="a60ff-173">Copy activity properties</span></span>
<span data-ttu-id="a60ff-174">Bölümleri ve etkinlikleri tanımlamak için kullanılabilir olan özellikleri tam listesi için bkz: [ardışık düzen oluşturma](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="a60ff-174">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a60ff-175">Ad, açıklama, giriş ve çıkış tabloları özellikler gibi ve çeşitli ilkeleri etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a60ff-175">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="a60ff-176">Etkinlik typeProperties bölümünde özellikler, diğer yandan, her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="a60ff-176">The properties that are available in the typeProperties section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="a60ff-177">Kopya etkinliği için bunlar türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="a60ff-177">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="a60ff-178">Kopyalama etkinliğinde kaynak türü olduğunda **RelationalSource** (içeren Salesforce), aşağıdaki özellikler typeProperties bölümünde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="a60ff-178">In copy activity, when the source is of the type **RelationalSource** (which includes Salesforce), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="a60ff-179">Özellik</span><span class="sxs-lookup"><span data-stu-id="a60ff-179">Property</span></span> | <span data-ttu-id="a60ff-180">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a60ff-180">Description</span></span> | <span data-ttu-id="a60ff-181">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="a60ff-181">Allowed values</span></span> | <span data-ttu-id="a60ff-182">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a60ff-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a60ff-183">sorgu</span><span class="sxs-lookup"><span data-stu-id="a60ff-183">query</span></span> |<span data-ttu-id="a60ff-184">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="a60ff-184">Use the custom query to read data.</span></span> |<span data-ttu-id="a60ff-185">Bir SQL-92 sorgu veya [Salesforce nesnesi sorgu dili (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) sorgu.</span><span class="sxs-lookup"><span data-stu-id="a60ff-185">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="a60ff-186">Örneğin:  `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="a60ff-186">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="a60ff-187">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="a60ff-187">No (if the **tableName** of the **dataset** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="a60ff-188">API adı "__c" bölümü için herhangi bir özel nesne gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a60ff-188">The "__c" part of the API Name is needed for any custom object.</span></span>

![Veri Fabrikası - Salesforce bağlantı - API adı](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="a60ff-190">Sorgu ipuçları</span><span class="sxs-lookup"><span data-stu-id="a60ff-190">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="a60ff-191">WHERE kullanarak veri alma DateTime sütun yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="a60ff-191">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="a60ff-192">Ne zaman SOQL veya SQL sorgusu DateTime biçimi fark dikkat belirtin.</span><span class="sxs-lookup"><span data-stu-id="a60ff-192">When specify the SOQL or SQL query, pay attention to the DateTime format difference.</span></span> <span data-ttu-id="a60ff-193">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a60ff-193">For example:</span></span>

* <span data-ttu-id="a60ff-194">**SOQL örnek**:`$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="a60ff-194">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="a60ff-195">**SQL örneği**:</span><span class="sxs-lookup"><span data-stu-id="a60ff-195">**SQL sample**:</span></span>
    * <span data-ttu-id="a60ff-196">**Sorgu belirtmek için kopyalama Sihirbazı'nı kullanarak:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="a60ff-196">**Using copy wizard to specify the query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="a60ff-197">**Sorgu belirtmek için düzenleme JSON kullanarak (char düzgün kaçış):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="a60ff-197">**Using JSON editing to specify the query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="a60ff-198">Salesforce raporundan veri alma</span><span class="sxs-lookup"><span data-stu-id="a60ff-198">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="a60ff-199">Sorgu olarak belirterek Salesforce raporlarını veri alabilirsiniz `{call "<report name>"}`, örneğin,.</span><span class="sxs-lookup"><span data-stu-id="a60ff-199">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="a60ff-200">`"query": "{call \"TestReport\"}"`.</span><span class="sxs-lookup"><span data-stu-id="a60ff-200">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="a60ff-201">Kayıtları Salesforce Geri Dönüşüm Kutusu'ndan silinen alma</span><span class="sxs-lookup"><span data-stu-id="a60ff-201">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="a60ff-202">Salesforce geri dönüşüm kutusu geçici silinen kayıtlarını sorgulamak için belirleyebileceğiniz **"IsDeleted = 1"** Sorgunuzdaki.</span><span class="sxs-lookup"><span data-stu-id="a60ff-202">To query the soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="a60ff-203">Örneğin,</span><span class="sxs-lookup"><span data-stu-id="a60ff-203">For example,</span></span>

* <span data-ttu-id="a60ff-204">Yalnızca Silinmiş kayıtlar sorgulamaya belirtin "seçin * MyTable__c gelen **burada IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="a60ff-204">To query only the deleted records, specify "select * from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="a60ff-205">Tüm mevcut ve Silinen dahil olmak üzere kayıtlarını sorgulamak üzere belirtin "seçin * MyTable__c gelen **burada IsDeleted = 0 ya da IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="a60ff-205">To query all the records including the existing and the deleted, specify "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-to-azure-blob"></a><span data-ttu-id="a60ff-206">JSON örnek: veri kopyalama Salesforce Azure Blob</span><span class="sxs-lookup"><span data-stu-id="a60ff-206">JSON example: Copy data from Salesforce to Azure Blob</span></span>
<span data-ttu-id="a60ff-207">Aşağıdaki örneği kullanarak bir işlem hattı oluşturmak için kullanabileceğiniz örnek JSON tanımları sağlar, [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a60ff-207">The following example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="a60ff-208">Bunlar Azure Blob depolama alanına Salesforce verileri kopyalamak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="a60ff-208">They show how to copy data from Salesforce to Azure Blob Storage.</span></span> <span data-ttu-id="a60ff-209">Ancak, veri herhangi belirtildiği havuzlarını kopyalanabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kopya etkinliği Azure Data Factory kullanarak.</span><span class="sxs-lookup"><span data-stu-id="a60ff-209">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="a60ff-210">Burada, senaryoyu uygulamak için oluşturmanız gerekecek Data Factory yapıtlarının bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a60ff-210">Here are the Data Factory artifacts that you'll need to create to implement the scenario.</span></span> <span data-ttu-id="a60ff-211">Listede zleyen Bu adımlar hakkında ayrıntılı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a60ff-211">The sections that follow the list provide details about these steps.</span></span>

* <span data-ttu-id="a60ff-212">Bağlı hizmet türü [Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="a60ff-212">A linked service of the type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="a60ff-213">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="a60ff-213">A linked service of the type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="a60ff-214">Bir giriş [dataset](data-factory-create-datasets.md) türü [RelationalTable](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="a60ff-214">An input [dataset](data-factory-create-datasets.md) of the type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="a60ff-215">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="a60ff-215">An output [dataset](data-factory-create-datasets.md) of the type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="a60ff-216">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="a60ff-216">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="a60ff-217">**Salesforce bağlı hizmet**</span><span class="sxs-lookup"><span data-stu-id="a60ff-217">**Salesforce linked service**</span></span>

<span data-ttu-id="a60ff-218">Bu örnekte **Salesforce** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="a60ff-218">This example uses the **Salesforce** linked service.</span></span> <span data-ttu-id="a60ff-219">Bkz: [Salesforce bağlantılı hizmeti](#linked-service-properties) bu bağlantılı hizmet tarafından desteklenen özellikler bölümü.</span><span class="sxs-lookup"><span data-stu-id="a60ff-219">See the [Salesforce linked service](#linked-service-properties) section for the properties that are supported by this linked service.</span></span>  <span data-ttu-id="a60ff-220">Bkz: [güvenlik belirteci alma getirin](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) sıfırlama/güvenlik belirteci alma hakkında yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="a60ff-220">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get the security token.</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```
<span data-ttu-id="a60ff-221">**Azure Storage bağlı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="a60ff-221">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="a60ff-222">**Salesforce girdi veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="a60ff-222">**Salesforce input dataset**</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
        },
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

<span data-ttu-id="a60ff-223">Ayarı **dış** için **true** Data Factory hizmetinin veri kümesi data factory dış ve veri fabrikasında bir etkinlik tarafından üretilen değil bildirir.</span><span class="sxs-lookup"><span data-stu-id="a60ff-223">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a60ff-224">API adı "__c" bölümü için herhangi bir özel nesne gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a60ff-224">The "__c" part of the API Name is needed for any custom object.</span></span>

![Veri Fabrikası - Salesforce bağlantı - API adı](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="a60ff-226">**Azure Blob çıktı veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="a60ff-226">**Azure blob output dataset**</span></span>

<span data-ttu-id="a60ff-227">Veri her saat yeni bir bloba yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="a60ff-227">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="a60ff-228">**Kopyalama etkinliği ile işlem hattı**</span><span class="sxs-lookup"><span data-stu-id="a60ff-228">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="a60ff-229">Ardışık Düzen giriş ve çıkış veri kümeleri kullanmak üzere yapılandırılmış ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="a60ff-229">The pipeline contains Copy Activity, which is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="a60ff-230">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **RelationalSource**ve **havuz** türü ayarlanmış **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a60ff-230">In the pipeline JSON definition, the **source** type is set to **RelationalSource**, and the **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="a60ff-231">Bkz: [RelationalSource türü özellikleri](#copy-activity-properties) RelationalSource tarafından desteklenen özelliklerin listesi için.</span><span class="sxs-lookup"><span data-stu-id="a60ff-231">See [RelationalSource type properties](#copy-activity-properties) for the list of properties that are supported by the RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce to an Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
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
> [!IMPORTANT]
> <span data-ttu-id="a60ff-232">API adı "__c" bölümü için herhangi bir özel nesne gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a60ff-232">The "__c" part of the API Name is needed for any custom object.</span></span>

![Veri Fabrikası - Salesforce bağlantı - API adı](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="a60ff-234">Tür eşlemesi için Salesforce</span><span class="sxs-lookup"><span data-stu-id="a60ff-234">Type mapping for Salesforce</span></span>
| <span data-ttu-id="a60ff-235">Salesforce türü</span><span class="sxs-lookup"><span data-stu-id="a60ff-235">Salesforce type</span></span> | <span data-ttu-id="a60ff-236">. NET tabanlı türü</span><span class="sxs-lookup"><span data-stu-id="a60ff-236">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="a60ff-237">Otomatik numara</span><span class="sxs-lookup"><span data-stu-id="a60ff-237">Auto Number</span></span> |<span data-ttu-id="a60ff-238">Dize</span><span class="sxs-lookup"><span data-stu-id="a60ff-238">String</span></span> |
| <span data-ttu-id="a60ff-239">Onay kutusu</span><span class="sxs-lookup"><span data-stu-id="a60ff-239">Checkbox</span></span> |<span data-ttu-id="a60ff-240">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="a60ff-240">Boolean</span></span> |
| <span data-ttu-id="a60ff-241">Para birimi</span><span class="sxs-lookup"><span data-stu-id="a60ff-241">Currency</span></span> |<span data-ttu-id="a60ff-242">Çift</span><span class="sxs-lookup"><span data-stu-id="a60ff-242">Double</span></span> |
| <span data-ttu-id="a60ff-243">Tarih</span><span class="sxs-lookup"><span data-stu-id="a60ff-243">Date</span></span> |<span data-ttu-id="a60ff-244">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="a60ff-244">DateTime</span></span> |
| <span data-ttu-id="a60ff-245">Tarih/saat</span><span class="sxs-lookup"><span data-stu-id="a60ff-245">Date/Time</span></span> |<span data-ttu-id="a60ff-246">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="a60ff-246">DateTime</span></span> |
| <span data-ttu-id="a60ff-247">E-posta</span><span class="sxs-lookup"><span data-stu-id="a60ff-247">Email</span></span> |<span data-ttu-id="a60ff-248">Dize</span><span class="sxs-lookup"><span data-stu-id="a60ff-248">String</span></span> |
| <span data-ttu-id="a60ff-249">Kimlik</span><span class="sxs-lookup"><span data-stu-id="a60ff-249">Id</span></span> |<span data-ttu-id="a60ff-250">Dize</span><span class="sxs-lookup"><span data-stu-id="a60ff-250">String</span></span> |
| <span data-ttu-id="a60ff-251">Arama ilişkisi</span><span class="sxs-lookup"><span data-stu-id="a60ff-251">Lookup Relationship</span></span> |<span data-ttu-id="a60ff-252">Dize</span><span class="sxs-lookup"><span data-stu-id="a60ff-252">String</span></span> |
| <span data-ttu-id="a60ff-253">Çoklu seçim seçim listesi</span><span class="sxs-lookup"><span data-stu-id="a60ff-253">Multi-Select Picklist</span></span> |<span data-ttu-id="a60ff-254">Dize</span><span class="sxs-lookup"><span data-stu-id="a60ff-254">String</span></span> |
| <span data-ttu-id="a60ff-255">Sayı</span><span class="sxs-lookup"><span data-stu-id="a60ff-255">Number</span></span> |<span data-ttu-id="a60ff-256">Çift</span><span class="sxs-lookup"><span data-stu-id="a60ff-256">Double</span></span> |
| <span data-ttu-id="a60ff-257">Yüzde</span><span class="sxs-lookup"><span data-stu-id="a60ff-257">Percent</span></span> |<span data-ttu-id="a60ff-258">Çift</span><span class="sxs-lookup"><span data-stu-id="a60ff-258">Double</span></span> |
| <span data-ttu-id="a60ff-259">Telefon</span><span class="sxs-lookup"><span data-stu-id="a60ff-259">Phone</span></span> |<span data-ttu-id="a60ff-260">Dize</span><span class="sxs-lookup"><span data-stu-id="a60ff-260">String</span></span> |
| <span data-ttu-id="a60ff-261">Seçim listesi</span><span class="sxs-lookup"><span data-stu-id="a60ff-261">Picklist</span></span> |<span data-ttu-id="a60ff-262">Dize</span><span class="sxs-lookup"><span data-stu-id="a60ff-262">String</span></span> |
| <span data-ttu-id="a60ff-263">Metin</span><span class="sxs-lookup"><span data-stu-id="a60ff-263">Text</span></span> |<span data-ttu-id="a60ff-264">Dize</span><span class="sxs-lookup"><span data-stu-id="a60ff-264">String</span></span> |
| <span data-ttu-id="a60ff-265">Metin alanı</span><span class="sxs-lookup"><span data-stu-id="a60ff-265">Text Area</span></span> |<span data-ttu-id="a60ff-266">Dize</span><span class="sxs-lookup"><span data-stu-id="a60ff-266">String</span></span> |
| <span data-ttu-id="a60ff-267">Metin alanı (uzun)</span><span class="sxs-lookup"><span data-stu-id="a60ff-267">Text Area (Long)</span></span> |<span data-ttu-id="a60ff-268">Dize</span><span class="sxs-lookup"><span data-stu-id="a60ff-268">String</span></span> |
| <span data-ttu-id="a60ff-269">Metin alanı (zengin)</span><span class="sxs-lookup"><span data-stu-id="a60ff-269">Text Area (Rich)</span></span> |<span data-ttu-id="a60ff-270">Dize</span><span class="sxs-lookup"><span data-stu-id="a60ff-270">String</span></span> |
| <span data-ttu-id="a60ff-271">Metin (şifrelenmiş)</span><span class="sxs-lookup"><span data-stu-id="a60ff-271">Text (Encrypted)</span></span> |<span data-ttu-id="a60ff-272">Dize</span><span class="sxs-lookup"><span data-stu-id="a60ff-272">String</span></span> |
| <span data-ttu-id="a60ff-273">URL</span><span class="sxs-lookup"><span data-stu-id="a60ff-273">URL</span></span> |<span data-ttu-id="a60ff-274">Dize</span><span class="sxs-lookup"><span data-stu-id="a60ff-274">String</span></span> |

> [!NOTE]
> <span data-ttu-id="a60ff-275">Kaynak veri kümesi sütunlarından havuz kümesinden sütunlara eşlemek için bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a60ff-275">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="a60ff-276">Performans ve ayar</span><span class="sxs-lookup"><span data-stu-id="a60ff-276">Performance and tuning</span></span>
<span data-ttu-id="a60ff-277">Bkz: [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md) bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve onu en iyi duruma getirmek için çeşitli yollar etkisi performansını anahtar Etkenler hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="a60ff-277">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
