---
title: "Veri Fabrikası kullanarak aaaMove verilerden Salesforce | Microsoft Docs"
description: "Hakkında bilgi edinin Azure Data Factory kullanarak toomove verilerden Salesforce."
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
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="da9a3-103">Azure Data Factory kullanarak Salesforce taşıma verileri</span><span class="sxs-lookup"><span data-stu-id="da9a3-103">Move data from Salesforce by using Azure Data Factory</span></span>
<span data-ttu-id="da9a3-104">Bu makalede Azure data factory toocopy veri Salesforce tooany veri deposundan hello havuz hello sütununda altında listelenen kopyalama etkinliği nasıl kullanabileceğiniz özetlenmektedir [desteklenen kaynakları ve havuzlarını](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="da9a3-104">This article outlines how you can use Copy Activity in an Azure data factory toocopy data from Salesforce tooany data store that is listed under hello Sink column in hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="da9a3-105">Bu makale üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) desteklenen veri deposu birleşimleri kopyalama etkinliği ile veri taşıma için genel bir bakış sunan makalesi.</span><span class="sxs-lookup"><span data-stu-id="da9a3-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="da9a3-106">Azure Data Factory şu anda destekler verileri Salesforce çok taşıma yalnızca[havuz veri depolarına desteklenen](data-factory-data-movement-activities.md#supported-data-stores-and-formats), ancak diğer veri depoları tooSalesforce gelen veri taşımayı desteklemez.</span><span class="sxs-lookup"><span data-stu-id="da9a3-106">Azure Data Factory currently supports only moving data from Salesforce too[supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores tooSalesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="da9a3-107">Desteklenen sürümler</span><span class="sxs-lookup"><span data-stu-id="da9a3-107">Supported versions</span></span>
<span data-ttu-id="da9a3-108">Bu bağlayıcı Salesforce sürümleri aşağıdaki hello destekler: Geliştirici sürümü, Professional Edition, Enterprise Edition veya sınırsız sürümü.</span><span class="sxs-lookup"><span data-stu-id="da9a3-108">This connector supports hello following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="da9a3-109">Ve Salesforce üretim, korumalı alan ve özel etki alanı kopyalama destekler.</span><span class="sxs-lookup"><span data-stu-id="da9a3-109">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da9a3-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="da9a3-110">Prerequisites</span></span>
* <span data-ttu-id="da9a3-111">API izni etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="da9a3-111">API permission must be enabled.</span></span> <span data-ttu-id="da9a3-112">Bkz: [nasıl Salesforce API erişim izni kümesi tarafından etkinleştirebilirim?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span><span class="sxs-lookup"><span data-stu-id="da9a3-112">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="da9a3-113">Salesforce tooon içi veri depolarına toocopy verileri, sahip olmanız gerekir en az veri yönetimi ağ geçidi şirket içi ortamınızda yüklü 2.0.</span><span class="sxs-lookup"><span data-stu-id="da9a3-113">toocopy data from Salesforce tooon-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="da9a3-114">Salesforce istek sınırları</span><span class="sxs-lookup"><span data-stu-id="da9a3-114">Salesforce request limits</span></span>
<span data-ttu-id="da9a3-115">Salesforce toplam API istekleri ve eşzamanlı API istekleri için sınırları vardır.</span><span class="sxs-lookup"><span data-stu-id="da9a3-115">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="da9a3-116">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="da9a3-116">Note hello following points:</span></span>

- <span data-ttu-id="da9a3-117">Eşzamanlı istek sayısını Hello hello sınırını aşarsa, azaltma gerçekleşir ve rastgele hatalara görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="da9a3-117">If hello number of concurrent requests exceeds hello limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="da9a3-118">Merhaba toplam istek sayısı hello sınırını aşarsa, 24 saat hello Salesforce hesap engellenir.</span><span class="sxs-lookup"><span data-stu-id="da9a3-118">If hello total number of requests exceeds hello limit, hello Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="da9a3-119">Ayrıca, her iki senaryoda hello "REQUEST_LIMIT_EXCEEDED" hatası alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da9a3-119">You might also receive hello “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="da9a3-120">Merhaba Hello "API istek sınırlarını" bölümüne bakın [Salesforce Geliştirici sınırları](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="da9a3-120">See hello "API Request Limits" section in hello [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="da9a3-121">Başlarken</span><span class="sxs-lookup"><span data-stu-id="da9a3-121">Getting started</span></span>
<span data-ttu-id="da9a3-122">Farklı araçlar/API'lerini kullanarak Salesforce verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="da9a3-122">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="da9a3-123">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="da9a3-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="da9a3-124">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="da9a3-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="da9a3-125">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="da9a3-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="da9a3-126">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="da9a3-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="da9a3-127">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="da9a3-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="da9a3-128">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="da9a3-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="da9a3-129">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="da9a3-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="da9a3-130">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="da9a3-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="da9a3-131">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="da9a3-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="da9a3-132">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="da9a3-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="da9a3-133">Salesforce kullanılan toocopy veri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: Blob Salesforce tooAzure veri kopyalama](#json-example-copy-data-from-salesforce-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="da9a3-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from Salesforce, see [JSON example: Copy data from Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="da9a3-134">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooSalesforce olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="da9a3-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSalesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="da9a3-135">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="da9a3-135">Linked service properties</span></span>
<span data-ttu-id="da9a3-136">Aşağıdaki tablonun hello belirli toohello Salesforce bağlantılı hizmet JSON öğeleri için açıklamalar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="da9a3-136">hello following table provides descriptions for JSON elements that are specific toohello Salesforce linked service.</span></span>

| <span data-ttu-id="da9a3-137">Özellik</span><span class="sxs-lookup"><span data-stu-id="da9a3-137">Property</span></span> | <span data-ttu-id="da9a3-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="da9a3-138">Description</span></span> | <span data-ttu-id="da9a3-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="da9a3-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="da9a3-140">type</span><span class="sxs-lookup"><span data-stu-id="da9a3-140">type</span></span> |<span data-ttu-id="da9a3-141">Merhaba type özelliği ayarlanmalıdır: **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="da9a3-141">hello type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="da9a3-142">Evet</span><span class="sxs-lookup"><span data-stu-id="da9a3-142">Yes</span></span> |
| <span data-ttu-id="da9a3-143">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="da9a3-143">environmentUrl</span></span> | <span data-ttu-id="da9a3-144">Merhaba, URL Salesforce örneği belirtin.</span><span class="sxs-lookup"><span data-stu-id="da9a3-144">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="da9a3-145">-Varsayılan değer "https://login.salesforce.com" dir.</span><span class="sxs-lookup"><span data-stu-id="da9a3-145">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="da9a3-146">-Korumalı alan, toocopy verileri "https://test.salesforce.com" belirtin.</span><span class="sxs-lookup"><span data-stu-id="da9a3-146">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="da9a3-147">-toocopy verileri özel bir etki alanından belirtin, örneğin, "https://[domain].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="da9a3-147">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="da9a3-148">Hayır</span><span class="sxs-lookup"><span data-stu-id="da9a3-148">No</span></span> |
| <span data-ttu-id="da9a3-149">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="da9a3-149">username</span></span> |<span data-ttu-id="da9a3-150">Merhaba kullanıcı hesabı için bir kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="da9a3-150">Specify a user name for hello user account.</span></span> |<span data-ttu-id="da9a3-151">Evet</span><span class="sxs-lookup"><span data-stu-id="da9a3-151">Yes</span></span> |
| <span data-ttu-id="da9a3-152">password</span><span class="sxs-lookup"><span data-stu-id="da9a3-152">password</span></span> |<span data-ttu-id="da9a3-153">Merhaba kullanıcı hesabı için bir parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="da9a3-153">Specify a password for hello user account.</span></span> |<span data-ttu-id="da9a3-154">Evet</span><span class="sxs-lookup"><span data-stu-id="da9a3-154">Yes</span></span> |
| <span data-ttu-id="da9a3-155">securityToken</span><span class="sxs-lookup"><span data-stu-id="da9a3-155">securityToken</span></span> |<span data-ttu-id="da9a3-156">Merhaba kullanıcı hesabı için bir güvenlik belirteci belirtin.</span><span class="sxs-lookup"><span data-stu-id="da9a3-156">Specify a security token for hello user account.</span></span> <span data-ttu-id="da9a3-157">Bkz: [güvenlik belirteci alma getirin](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) yönelik yönergeler tooreset/get bir güvenlik belirteci.</span><span class="sxs-lookup"><span data-stu-id="da9a3-157">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="da9a3-158">Genel olarak, toolearn güvenlik belirteçleri hakkında bkz [güvenlik ve hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="da9a3-158">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="da9a3-159">Evet</span><span class="sxs-lookup"><span data-stu-id="da9a3-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="da9a3-160">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="da9a3-160">Dataset properties</span></span>
<span data-ttu-id="da9a3-161">Merhaba bölümler ve veri kümelerini tanımlamak için kullanılabilir olan özellikleri tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="da9a3-161">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="da9a3-162">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri kümesi türleri için (Azure SQL, Azure blob, Azure tablo ve benzeri) benzer.</span><span class="sxs-lookup"><span data-stu-id="da9a3-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="da9a3-163">Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="da9a3-163">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="da9a3-164">Merhaba typeProperties bölümünde hello türü veri kümesi için **RelationalTable** hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="da9a3-164">hello typeProperties section for a dataset of hello type **RelationalTable** has hello following properties:</span></span>

| <span data-ttu-id="da9a3-165">Özellik</span><span class="sxs-lookup"><span data-stu-id="da9a3-165">Property</span></span> | <span data-ttu-id="da9a3-166">Açıklama</span><span class="sxs-lookup"><span data-stu-id="da9a3-166">Description</span></span> | <span data-ttu-id="da9a3-167">Gerekli</span><span class="sxs-lookup"><span data-stu-id="da9a3-167">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="da9a3-168">tableName</span><span class="sxs-lookup"><span data-stu-id="da9a3-168">tableName</span></span> |<span data-ttu-id="da9a3-169">Salesforce Merhaba tablonun adı.</span><span class="sxs-lookup"><span data-stu-id="da9a3-169">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="da9a3-170">Hayır (varsa bir **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="da9a3-170">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="da9a3-171">Merhaba "__c" Merhaba API adı parçası herhangi bir özel nesnesi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="da9a3-171">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Veri Fabrikası - Salesforce bağlantı - API adı](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="da9a3-173">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="da9a3-173">Copy activity properties</span></span>
<span data-ttu-id="da9a3-174">Merhaba bölümler ve etkinlikleri tanımlamak için kullanılabilir olan özellikleri tam listesi için bkz [ardışık düzen oluşturma](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="da9a3-174">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="da9a3-175">Ad, açıklama, giriş ve çıkış tabloları özellikler gibi ve çeşitli ilkeleri etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="da9a3-175">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="da9a3-176">kullanılabilir hello özellikleri hello faaliyete hello typeProperties bölümünü diğer yandan Merhaba, her etkinlik türü ile değişir.</span><span class="sxs-lookup"><span data-stu-id="da9a3-176">hello properties that are available in hello typeProperties section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="da9a3-177">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="da9a3-177">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="da9a3-178">Kopyalama etkinliğinde hello kaynağı hello türü olduğunda **RelationalSource** (içeren Salesforce), aşağıdaki özelliklere hello typeProperties bölümünde bulunur:</span><span class="sxs-lookup"><span data-stu-id="da9a3-178">In copy activity, when hello source is of hello type **RelationalSource** (which includes Salesforce), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="da9a3-179">Özellik</span><span class="sxs-lookup"><span data-stu-id="da9a3-179">Property</span></span> | <span data-ttu-id="da9a3-180">Açıklama</span><span class="sxs-lookup"><span data-stu-id="da9a3-180">Description</span></span> | <span data-ttu-id="da9a3-181">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="da9a3-181">Allowed values</span></span> | <span data-ttu-id="da9a3-182">Gerekli</span><span class="sxs-lookup"><span data-stu-id="da9a3-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="da9a3-183">sorgu</span><span class="sxs-lookup"><span data-stu-id="da9a3-183">query</span></span> |<span data-ttu-id="da9a3-184">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="da9a3-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="da9a3-185">Bir SQL-92 sorgu veya [Salesforce nesnesi sorgu dili (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) sorgu.</span><span class="sxs-lookup"><span data-stu-id="da9a3-185">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="da9a3-186">Örneğin:  `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="da9a3-186">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="da9a3-187">Hayır (Merhaba, **tableName** Merhaba, **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="da9a3-187">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="da9a3-188">Merhaba "__c" Merhaba API adı parçası herhangi bir özel nesnesi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="da9a3-188">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Veri Fabrikası - Salesforce bağlantı - API adı](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="da9a3-190">Sorgu ipuçları</span><span class="sxs-lookup"><span data-stu-id="da9a3-190">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="da9a3-191">WHERE kullanarak veri alma DateTime sütun yan tümcesi</span><span class="sxs-lookup"><span data-stu-id="da9a3-191">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="da9a3-192">Ne zaman hello SOQL veya SQL sorgusu, ödeme dikkat toohello DateTime biçimi fark belirtin.</span><span class="sxs-lookup"><span data-stu-id="da9a3-192">When specify hello SOQL or SQL query, pay attention toohello DateTime format difference.</span></span> <span data-ttu-id="da9a3-193">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="da9a3-193">For example:</span></span>

* <span data-ttu-id="da9a3-194">**SOQL örnek**:`$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="da9a3-194">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="da9a3-195">**SQL örneği**:</span><span class="sxs-lookup"><span data-stu-id="da9a3-195">**SQL sample**:</span></span>
    * <span data-ttu-id="da9a3-196">**Kopyalama Sihirbazı'nı toospecify hello sorgu kullanarak:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="da9a3-196">**Using copy wizard toospecify hello query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="da9a3-197">**JSON toospecify hello sorgu düzenlemeye kullanarak (char düzgün kaçış):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="da9a3-197">**Using JSON editing toospecify hello query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="da9a3-198">Salesforce raporundan veri alma</span><span class="sxs-lookup"><span data-stu-id="da9a3-198">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="da9a3-199">Sorgu olarak belirterek Salesforce raporlarını veri alabilirsiniz `{call "<report name>"}`, örneğin,.</span><span class="sxs-lookup"><span data-stu-id="da9a3-199">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="da9a3-200">`"query": "{call \"TestReport\"}"`.</span><span class="sxs-lookup"><span data-stu-id="da9a3-200">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="da9a3-201">Kayıtları Salesforce Geri Dönüşüm Kutusu'ndan silinen alma</span><span class="sxs-lookup"><span data-stu-id="da9a3-201">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="da9a3-202">Salesforce geri dönüşüm kutusu tooquery hello yumuşak silinmiş kayıtları, belirtebilirsiniz **"IsDeleted = 1"** Sorgunuzdaki.</span><span class="sxs-lookup"><span data-stu-id="da9a3-202">tooquery hello soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="da9a3-203">Örneğin,</span><span class="sxs-lookup"><span data-stu-id="da9a3-203">For example,</span></span>

* <span data-ttu-id="da9a3-204">tooquery yalnızca hello silinmiş kayıtlar belirtin "seçin * MyTable__c gelen **burada IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="da9a3-204">tooquery only hello deleted records, specify "select * from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="da9a3-205">Tüm hello hello mevcut ve Silinen, hello dahil olmak üzere kayıtları tooquery belirtin "seçin * MyTable__c gelen **burada IsDeleted = 0 ya da IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="da9a3-205">tooquery all hello records including hello existing and hello deleted, specify "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a><span data-ttu-id="da9a3-206">JSON örnek: Blob Salesforce tooAzure veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="da9a3-206">JSON example: Copy data from Salesforce tooAzure Blob</span></span>
<span data-ttu-id="da9a3-207">Merhaba aşağıdaki örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen hello kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="da9a3-207">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="da9a3-208">Bunlar Göster nasıl Salesforce tooAzure Blob Storage toocopy verileri.</span><span class="sxs-lookup"><span data-stu-id="da9a3-208">They show how toocopy data from Salesforce tooAzure Blob Storage.</span></span> <span data-ttu-id="da9a3-209">Ancak, veri belirtildiği hello havuzlarını, kopyalanan tooany olabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="da9a3-209">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="da9a3-210">Burada, toocreate tooimplement hello senaryo gerekir hello Data Factory yapıtlarının bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="da9a3-210">Here are hello Data Factory artifacts that you'll need toocreate tooimplement hello scenario.</span></span> <span data-ttu-id="da9a3-211">Merhaba listesini izleyen hello bölümler bu adımlar hakkında ayrıntılı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="da9a3-211">hello sections that follow hello list provide details about these steps.</span></span>

* <span data-ttu-id="da9a3-212">Merhaba türündeki bağlı hizmetin [Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="da9a3-212">A linked service of hello type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="da9a3-213">Merhaba türündeki bağlı hizmetin [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="da9a3-213">A linked service of hello type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="da9a3-214">Bir giriş [dataset](data-factory-create-datasets.md) hello türü [RelationalTable](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="da9a3-214">An input [dataset](data-factory-create-datasets.md) of hello type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="da9a3-215">Bir çıkış [dataset](data-factory-create-datasets.md) hello türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="da9a3-215">An output [dataset](data-factory-create-datasets.md) of hello type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="da9a3-216">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="da9a3-216">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="da9a3-217">**Salesforce bağlı hizmet**</span><span class="sxs-lookup"><span data-stu-id="da9a3-217">**Salesforce linked service**</span></span>

<span data-ttu-id="da9a3-218">Bu örnek hello kullanır **Salesforce** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="da9a3-218">This example uses hello **Salesforce** linked service.</span></span> <span data-ttu-id="da9a3-219">Merhaba bkz [Salesforce bağlantılı hizmeti](#linked-service-properties) bu bağlantılı hizmet tarafından desteklenen hello özellikler bölümü.</span><span class="sxs-lookup"><span data-stu-id="da9a3-219">See hello [Salesforce linked service](#linked-service-properties) section for hello properties that are supported by this linked service.</span></span>  <span data-ttu-id="da9a3-220">Bkz: [güvenlik belirteci alma getirin](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) nasıl tooreset/get hello güvenlik belirteci hakkında yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="da9a3-220">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get hello security token.</span></span>

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
<span data-ttu-id="da9a3-221">**Azure Storage bağlı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="da9a3-221">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="da9a3-222">**Salesforce girdi veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="da9a3-222">**Salesforce input dataset**</span></span>

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

<span data-ttu-id="da9a3-223">Ayarı **dış** çok**true** hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil bildirir.</span><span class="sxs-lookup"><span data-stu-id="da9a3-223">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da9a3-224">Merhaba "__c" Merhaba API adı parçası herhangi bir özel nesnesi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="da9a3-224">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Veri Fabrikası - Salesforce bağlantı - API adı](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="da9a3-226">**Azure Blob çıktı veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="da9a3-226">**Azure blob output dataset**</span></span>

<span data-ttu-id="da9a3-227">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="da9a3-227">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

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

<span data-ttu-id="da9a3-228">**Kopyalama etkinliği ile işlem hattı**</span><span class="sxs-lookup"><span data-stu-id="da9a3-228">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="da9a3-229">Merhaba ardışık düzen içeren yapılandırılmış kopyalama etkinliği toouse girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="da9a3-229">hello pipeline contains Copy Activity, which is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="da9a3-230">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**RelationalSource**ve hello **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="da9a3-230">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource**, and hello **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="da9a3-231">Bkz: [RelationalSource türü özellikleri](#copy-activity-properties) hello RelationalSource hello tarafından desteklenen özelliklerin listesi için.</span><span class="sxs-lookup"><span data-stu-id="da9a3-231">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties that are supported by hello RelationalSource.</span></span>

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
            "description": "Copy from Salesforce tooan Azure blob",
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
> <span data-ttu-id="da9a3-232">Merhaba "__c" Merhaba API adı parçası herhangi bir özel nesnesi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="da9a3-232">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Veri Fabrikası - Salesforce bağlantı - API adı](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="da9a3-234">Tür eşlemesi için Salesforce</span><span class="sxs-lookup"><span data-stu-id="da9a3-234">Type mapping for Salesforce</span></span>
| <span data-ttu-id="da9a3-235">Salesforce türü</span><span class="sxs-lookup"><span data-stu-id="da9a3-235">Salesforce type</span></span> | <span data-ttu-id="da9a3-236">. NET tabanlı türü</span><span class="sxs-lookup"><span data-stu-id="da9a3-236">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="da9a3-237">Otomatik numara</span><span class="sxs-lookup"><span data-stu-id="da9a3-237">Auto Number</span></span> |<span data-ttu-id="da9a3-238">Dize</span><span class="sxs-lookup"><span data-stu-id="da9a3-238">String</span></span> |
| <span data-ttu-id="da9a3-239">Onay kutusu</span><span class="sxs-lookup"><span data-stu-id="da9a3-239">Checkbox</span></span> |<span data-ttu-id="da9a3-240">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="da9a3-240">Boolean</span></span> |
| <span data-ttu-id="da9a3-241">Para birimi</span><span class="sxs-lookup"><span data-stu-id="da9a3-241">Currency</span></span> |<span data-ttu-id="da9a3-242">Çift</span><span class="sxs-lookup"><span data-stu-id="da9a3-242">Double</span></span> |
| <span data-ttu-id="da9a3-243">Tarih</span><span class="sxs-lookup"><span data-stu-id="da9a3-243">Date</span></span> |<span data-ttu-id="da9a3-244">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="da9a3-244">DateTime</span></span> |
| <span data-ttu-id="da9a3-245">Tarih/saat</span><span class="sxs-lookup"><span data-stu-id="da9a3-245">Date/Time</span></span> |<span data-ttu-id="da9a3-246">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="da9a3-246">DateTime</span></span> |
| <span data-ttu-id="da9a3-247">E-posta</span><span class="sxs-lookup"><span data-stu-id="da9a3-247">Email</span></span> |<span data-ttu-id="da9a3-248">Dize</span><span class="sxs-lookup"><span data-stu-id="da9a3-248">String</span></span> |
| <span data-ttu-id="da9a3-249">Kimlik</span><span class="sxs-lookup"><span data-stu-id="da9a3-249">Id</span></span> |<span data-ttu-id="da9a3-250">Dize</span><span class="sxs-lookup"><span data-stu-id="da9a3-250">String</span></span> |
| <span data-ttu-id="da9a3-251">Arama ilişkisi</span><span class="sxs-lookup"><span data-stu-id="da9a3-251">Lookup Relationship</span></span> |<span data-ttu-id="da9a3-252">Dize</span><span class="sxs-lookup"><span data-stu-id="da9a3-252">String</span></span> |
| <span data-ttu-id="da9a3-253">Çoklu seçim seçim listesi</span><span class="sxs-lookup"><span data-stu-id="da9a3-253">Multi-Select Picklist</span></span> |<span data-ttu-id="da9a3-254">Dize</span><span class="sxs-lookup"><span data-stu-id="da9a3-254">String</span></span> |
| <span data-ttu-id="da9a3-255">Sayı</span><span class="sxs-lookup"><span data-stu-id="da9a3-255">Number</span></span> |<span data-ttu-id="da9a3-256">Çift</span><span class="sxs-lookup"><span data-stu-id="da9a3-256">Double</span></span> |
| <span data-ttu-id="da9a3-257">Yüzde</span><span class="sxs-lookup"><span data-stu-id="da9a3-257">Percent</span></span> |<span data-ttu-id="da9a3-258">Çift</span><span class="sxs-lookup"><span data-stu-id="da9a3-258">Double</span></span> |
| <span data-ttu-id="da9a3-259">Telefon</span><span class="sxs-lookup"><span data-stu-id="da9a3-259">Phone</span></span> |<span data-ttu-id="da9a3-260">Dize</span><span class="sxs-lookup"><span data-stu-id="da9a3-260">String</span></span> |
| <span data-ttu-id="da9a3-261">Seçim listesi</span><span class="sxs-lookup"><span data-stu-id="da9a3-261">Picklist</span></span> |<span data-ttu-id="da9a3-262">Dize</span><span class="sxs-lookup"><span data-stu-id="da9a3-262">String</span></span> |
| <span data-ttu-id="da9a3-263">Metin</span><span class="sxs-lookup"><span data-stu-id="da9a3-263">Text</span></span> |<span data-ttu-id="da9a3-264">Dize</span><span class="sxs-lookup"><span data-stu-id="da9a3-264">String</span></span> |
| <span data-ttu-id="da9a3-265">Metin alanı</span><span class="sxs-lookup"><span data-stu-id="da9a3-265">Text Area</span></span> |<span data-ttu-id="da9a3-266">Dize</span><span class="sxs-lookup"><span data-stu-id="da9a3-266">String</span></span> |
| <span data-ttu-id="da9a3-267">Metin alanı (uzun)</span><span class="sxs-lookup"><span data-stu-id="da9a3-267">Text Area (Long)</span></span> |<span data-ttu-id="da9a3-268">Dize</span><span class="sxs-lookup"><span data-stu-id="da9a3-268">String</span></span> |
| <span data-ttu-id="da9a3-269">Metin alanı (zengin)</span><span class="sxs-lookup"><span data-stu-id="da9a3-269">Text Area (Rich)</span></span> |<span data-ttu-id="da9a3-270">Dize</span><span class="sxs-lookup"><span data-stu-id="da9a3-270">String</span></span> |
| <span data-ttu-id="da9a3-271">Metin (şifrelenmiş)</span><span class="sxs-lookup"><span data-stu-id="da9a3-271">Text (Encrypted)</span></span> |<span data-ttu-id="da9a3-272">Dize</span><span class="sxs-lookup"><span data-stu-id="da9a3-272">String</span></span> |
| <span data-ttu-id="da9a3-273">URL</span><span class="sxs-lookup"><span data-stu-id="da9a3-273">URL</span></span> |<span data-ttu-id="da9a3-274">Dize</span><span class="sxs-lookup"><span data-stu-id="da9a3-274">String</span></span> |

> [!NOTE]
> <span data-ttu-id="da9a3-275">Kaynak veri kümesi toocolumns havuz kümesinden toomap sütunlarından bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="da9a3-275">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="da9a3-276">Performans ve ayar</span><span class="sxs-lookup"><span data-stu-id="da9a3-276">Performance and tuning</span></span>
<span data-ttu-id="da9a3-277">Merhaba bkz [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="da9a3-277">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
