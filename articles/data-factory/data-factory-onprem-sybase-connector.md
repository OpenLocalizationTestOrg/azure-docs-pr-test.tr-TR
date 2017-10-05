---
title: "Azure Data Factory kullanarak Sybase'den veri taşıma | Microsoft Docs"
description: "Azure Data Factory kullanarak Sybase veritabanından veri taşıma hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: b379ee10-0ff5-4974-8c87-c95f82f1c5c6
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 617e604b220b8bc1c452e67da83f733448e16c0b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="79dfd-103">Azure Data Factory kullanarak Sybase taşıma verileri</span><span class="sxs-lookup"><span data-stu-id="79dfd-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="79dfd-104">Bu makalede kopya etkinliği Azure Data Factory'de bir şirket içi Sybase veritabanından veri taşımak için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="79dfd-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Sybase database.</span></span> <span data-ttu-id="79dfd-105">Derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) kopyalama etkinliği ile veri taşıma için genel bir bakış sunar makalesi.</span><span class="sxs-lookup"><span data-stu-id="79dfd-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="79dfd-106">Bir şirket içi Sybase veri deposundan verileri herhangi bir desteklenen havuz veri deposuna kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79dfd-106">You can copy data from an on-premises Sybase data store to any supported sink data store.</span></span> <span data-ttu-id="79dfd-107">Veri depoları havuzlarını kopyalama etkinliği tarafından desteklenen bir listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="79dfd-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="79dfd-108">Veri Fabrikası şu anda yalnızca veri taşımayı Sybase veri deposundan diğer veri depolarına, ancak verileri diğer veri depolarına bir Sybase veri deposuna taşıma değil destekler.</span><span class="sxs-lookup"><span data-stu-id="79dfd-108">Data factory currently supports only moving data from a Sybase data store to other data stores, but not for moving data from other data stores to a Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="79dfd-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="79dfd-109">Prerequisites</span></span>
<span data-ttu-id="79dfd-110">Data Factory hizmetinin şirket içi Sybase kaynaklarına veri yönetimi ağ geçidi kullanarak bağlanmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="79dfd-110">Data Factory service supports connecting to on-premises Sybase sources using the Data Management Gateway.</span></span> <span data-ttu-id="79dfd-111">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale veri yönetimi ağ geçidi ve ağ geçidi kurun ayarlama hakkında adım adım yönergeleri hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="79dfd-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="79dfd-112">Sybase veritabanına bir Azure Iaas sanal barındırılan olsa bile ağ geçidi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="79dfd-112">Gateway is required even if the Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="79dfd-113">Ağ geçidi veritabanına bağlanıp sürece veri deposu olarak aynı Iaas VM veya farklı bir VM ağ geçidi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79dfd-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="79dfd-114">Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="79dfd-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="79dfd-115">Desteklenen sürümleri ve yükleme</span><span class="sxs-lookup"><span data-stu-id="79dfd-115">Supported versions and installation</span></span>
<span data-ttu-id="79dfd-116">Veri Yönetimi Sybase veritabanına bağlanmak ağ geçidi için yüklemeniz gerekir. [Sybase iAnywhere.Data.SQLAnywhere için veri sağlayıcı](http://go.microsoft.com/fwlink/?linkid=324846) 16 veya üzeri veri yönetimi ağ geçidi ile aynı sistemde.</span><span class="sxs-lookup"><span data-stu-id="79dfd-116">For Data Management Gateway to connect to the Sybase Database, you need to install the [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="79dfd-117">Sybase sürüm 16 ve üzeri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="79dfd-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="79dfd-118">Başlarken</span><span class="sxs-lookup"><span data-stu-id="79dfd-118">Getting started</span></span>
<span data-ttu-id="79dfd-119">Farklı araçlar/API'lerini kullanarak bir şirket içi Cassandra veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="79dfd-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="79dfd-120">Bir işlem hattı oluşturmak için en kolay yolu kullanmaktır **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="79dfd-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="79dfd-121">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) veri kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="79dfd-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="79dfd-122">Bir işlem hattı oluşturmak için aşağıdaki araçları kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu**, **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="79dfd-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="79dfd-123">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="79dfd-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="79dfd-124">Araçlar ya da API'leri kullanıp bir havuz veri deposu için bir kaynak veri deposundan verileri taşır bir ardışık düzen oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="79dfd-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="79dfd-125">Oluşturma **bağlantılı Hizmetleri** girdi ve çıktı verilerini bağlamak için veri fabrikanıza depolar.</span><span class="sxs-lookup"><span data-stu-id="79dfd-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="79dfd-126">Oluşturma **veri kümeleri** kopyalama işlemi için girdi ve çıktı verilerini temsil etmek için.</span><span class="sxs-lookup"><span data-stu-id="79dfd-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="79dfd-127">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="79dfd-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="79dfd-128">Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="79dfd-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="79dfd-129">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, JSON biçimini kullanarak bu Data Factory varlıklarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="79dfd-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="79dfd-130">Bir şirket içi Sybase veri deposundan verileri kopyalamak için kullanılan Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: veri kopyalama Sybase'den Azure Blob](#json-example-copy-data-from-sybase-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="79dfd-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase to Azure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="79dfd-131">Aşağıdaki bölümler, Data Factory varlıklarını belirli bir Sybase veri deposuna tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="79dfd-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="79dfd-132">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="79dfd-132">Linked service properties</span></span>
<span data-ttu-id="79dfd-133">Aşağıdaki tabloda, JSON öğeleri Sybase bağlantılı hizmete özgü açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="79dfd-133">The following table provides description for JSON elements specific to Sybase linked service.</span></span>

| <span data-ttu-id="79dfd-134">Özellik</span><span class="sxs-lookup"><span data-stu-id="79dfd-134">Property</span></span> | <span data-ttu-id="79dfd-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="79dfd-135">Description</span></span> | <span data-ttu-id="79dfd-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="79dfd-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="79dfd-137">type</span><span class="sxs-lookup"><span data-stu-id="79dfd-137">type</span></span> |<span data-ttu-id="79dfd-138">Type özelliği ayarlanmalıdır: **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="79dfd-138">The type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="79dfd-139">Evet</span><span class="sxs-lookup"><span data-stu-id="79dfd-139">Yes</span></span> |
| <span data-ttu-id="79dfd-140">sunucu</span><span class="sxs-lookup"><span data-stu-id="79dfd-140">server</span></span> |<span data-ttu-id="79dfd-141">Sybase sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="79dfd-141">Name of the Sybase server.</span></span> |<span data-ttu-id="79dfd-142">Evet</span><span class="sxs-lookup"><span data-stu-id="79dfd-142">Yes</span></span> |
| <span data-ttu-id="79dfd-143">Veritabanı</span><span class="sxs-lookup"><span data-stu-id="79dfd-143">database</span></span> |<span data-ttu-id="79dfd-144">Sybase veritabanının adı.</span><span class="sxs-lookup"><span data-stu-id="79dfd-144">Name of the Sybase database.</span></span> |<span data-ttu-id="79dfd-145">Evet</span><span class="sxs-lookup"><span data-stu-id="79dfd-145">Yes</span></span> |
| <span data-ttu-id="79dfd-146">Şema</span><span class="sxs-lookup"><span data-stu-id="79dfd-146">schema</span></span> |<span data-ttu-id="79dfd-147">Veritabanı şemasında adı.</span><span class="sxs-lookup"><span data-stu-id="79dfd-147">Name of the schema in the database.</span></span> |<span data-ttu-id="79dfd-148">Hayır</span><span class="sxs-lookup"><span data-stu-id="79dfd-148">No</span></span> |
| <span data-ttu-id="79dfd-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="79dfd-149">authenticationType</span></span> |<span data-ttu-id="79dfd-150">Sybase veritabanına bağlanmak için kullanılan kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="79dfd-150">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="79dfd-151">Olası değerler şunlardır: Anonim, temel ve Windows.</span><span class="sxs-lookup"><span data-stu-id="79dfd-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="79dfd-152">Evet</span><span class="sxs-lookup"><span data-stu-id="79dfd-152">Yes</span></span> |
| <span data-ttu-id="79dfd-153">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="79dfd-153">username</span></span> |<span data-ttu-id="79dfd-154">Temel veya Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="79dfd-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="79dfd-155">Hayır</span><span class="sxs-lookup"><span data-stu-id="79dfd-155">No</span></span> |
| <span data-ttu-id="79dfd-156">password</span><span class="sxs-lookup"><span data-stu-id="79dfd-156">password</span></span> |<span data-ttu-id="79dfd-157">Kullanıcı adı için belirtilen kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="79dfd-157">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="79dfd-158">Hayır</span><span class="sxs-lookup"><span data-stu-id="79dfd-158">No</span></span> |
| <span data-ttu-id="79dfd-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="79dfd-159">gatewayName</span></span> |<span data-ttu-id="79dfd-160">Data Factory hizmetinin şirket içi Sybase veritabanına bağlanmak için kullanması gereken ağ geçidinin adı.</span><span class="sxs-lookup"><span data-stu-id="79dfd-160">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="79dfd-161">Evet</span><span class="sxs-lookup"><span data-stu-id="79dfd-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="79dfd-162">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="79dfd-162">Dataset properties</span></span>
<span data-ttu-id="79dfd-163">Bölümler & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="79dfd-163">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="79dfd-164">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="79dfd-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="79dfd-165">TypeProperties bölümü dataset her tür için farklıdır ve verilerin veri deposunda konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="79dfd-165">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="79dfd-166">**TypeProperties** veri kümesi için bir bölüm türü **RelationalTable** (Sybase veri kümesi içeren) aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="79dfd-166">The **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has the following properties:</span></span>

| <span data-ttu-id="79dfd-167">Özellik</span><span class="sxs-lookup"><span data-stu-id="79dfd-167">Property</span></span> | <span data-ttu-id="79dfd-168">Açıklama</span><span class="sxs-lookup"><span data-stu-id="79dfd-168">Description</span></span> | <span data-ttu-id="79dfd-169">Gerekli</span><span class="sxs-lookup"><span data-stu-id="79dfd-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="79dfd-170">tableName</span><span class="sxs-lookup"><span data-stu-id="79dfd-170">tableName</span></span> |<span data-ttu-id="79dfd-171">Sybase veritabanı örneğinde bağlantılı hizmet başvurduğu tablonun adı.</span><span class="sxs-lookup"><span data-stu-id="79dfd-171">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="79dfd-172">Hayır (varsa **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="79dfd-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="79dfd-173">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="79dfd-173">Copy activity properties</span></span>
<span data-ttu-id="79dfd-174">Bölümler & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz: [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="79dfd-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="79dfd-175">Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="79dfd-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="79dfd-176">Oysa etkinliğin typeProperties bölümündeki özellikler her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="79dfd-176">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="79dfd-177">Kopya etkinliği için bunlar türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="79dfd-177">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="79dfd-178">Kaynak türü olduğunda **RelationalSource** (içeren Sybase), aşağıdaki özellikler mevcuttur **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="79dfd-178">When the source is of type **RelationalSource** (which includes Sybase), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="79dfd-179">Özellik</span><span class="sxs-lookup"><span data-stu-id="79dfd-179">Property</span></span> | <span data-ttu-id="79dfd-180">Açıklama</span><span class="sxs-lookup"><span data-stu-id="79dfd-180">Description</span></span> | <span data-ttu-id="79dfd-181">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="79dfd-181">Allowed values</span></span> | <span data-ttu-id="79dfd-182">Gerekli</span><span class="sxs-lookup"><span data-stu-id="79dfd-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="79dfd-183">sorgu</span><span class="sxs-lookup"><span data-stu-id="79dfd-183">query</span></span> |<span data-ttu-id="79dfd-184">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="79dfd-184">Use the custom query to read data.</span></span> |<span data-ttu-id="79dfd-185">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="79dfd-185">SQL query string.</span></span> <span data-ttu-id="79dfd-186">Örneğin: seçin * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="79dfd-186">For example: select * from MyTable.</span></span> |<span data-ttu-id="79dfd-187">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="79dfd-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-to-azure-blob"></a><span data-ttu-id="79dfd-188">JSON örnek: veri kopyalama Sybase'den Azure Blob</span><span class="sxs-lookup"><span data-stu-id="79dfd-188">JSON example: Copy data from Sybase to Azure Blob</span></span>
<span data-ttu-id="79dfd-189">Aşağıdaki örneği kullanarak bir işlem hattı oluşturmak için kullanabileceğiniz örnek JSON tanımları sağlar, [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="79dfd-189">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="79dfd-190">Bunlar, verileri Azure Blob depolama alanına Sybase veritabanından kopyalamak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="79dfd-190">They show how to copy data from Sybase database to Azure Blob Storage.</span></span> <span data-ttu-id="79dfd-191">Ancak, veri herhangi belirtildiği havuzlarını kopyalanabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kopya etkinliği Azure Data Factory kullanarak.</span><span class="sxs-lookup"><span data-stu-id="79dfd-191">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="79dfd-192">Örnek aşağıdaki data factory varlıklarını sahiptir:</span><span class="sxs-lookup"><span data-stu-id="79dfd-192">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="79dfd-193">Bağlı hizmet türü [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="79dfd-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="79dfd-194">Türünde bir liked hizmet [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="79dfd-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="79dfd-195">Bir giriş [dataset](data-factory-create-datasets.md) türü [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="79dfd-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="79dfd-196">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="79dfd-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="79dfd-197">[Ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="79dfd-197">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="79dfd-198">Örnek veri Sybase veritabanında sorgu sonucu bir blobu saatte kopyalar.</span><span class="sxs-lookup"><span data-stu-id="79dfd-198">The sample copies data from a query result in Sybase database to a blob every hour.</span></span> <span data-ttu-id="79dfd-199">Bu örnekler kullanılan JSON özellikleri örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="79dfd-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="79dfd-200">İlk adım olarak, veri yönetimi ağ geçidi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="79dfd-200">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="79dfd-201">Yönergeler bulunan [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="79dfd-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="79dfd-202">**Sybase bağlantılı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="79dfd-202">**Sybase linked service:**</span></span>

```JSON
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="79dfd-203">**Azure Blob storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="79dfd-203">**Azure Blob storage linked service:**</span></span>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="79dfd-204">**Sybase girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="79dfd-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="79dfd-205">Örnek bir tablo "MyTable" Sybase içinde oluşturduğunuz ve zaman serisi veri için "zaman damgası" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="79dfd-205">The sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="79dfd-206">"Dış" ayarı: true, bu veri kümesi data factory dış ve veri fabrikasında bir etkinlik tarafından üretilen değil Data Factory hizmetinin bildirir.</span><span class="sxs-lookup"><span data-stu-id="79dfd-206">Setting “external”: true informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="79dfd-207">Dikkat **türü** bağlı hizmetin adı ayarlamak: **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="79dfd-207">Notice that the **type** of the linked service is set to: **RelationalTable**.</span></span>

```JSON
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
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

<span data-ttu-id="79dfd-208">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="79dfd-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="79dfd-209">Veri her saat yeni bir bloba yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="79dfd-209">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="79dfd-210">Blob klasör yolu dinamik işlenmekte olan dilim başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="79dfd-210">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="79dfd-211">Klasör yolu yıl, ay, gün ve saat bölümleri başlangıç saatini kullanır.</span><span class="sxs-lookup"><span data-stu-id="79dfd-211">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
    "name": "AzureBlobSybaseDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sybase/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="79dfd-212">**Kopyalama etkinliği ile kanal:**</span><span class="sxs-lookup"><span data-stu-id="79dfd-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="79dfd-213">Ardışık Düzen giriş ve çıkış veri kümeleri kullanmak üzere yapılandırılmış ve saatte bir çalışacak şekilde zamanlanmış bir kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="79dfd-213">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="79dfd-214">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **RelationalSource** ve **havuz** türü ayarlanmış **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="79dfd-214">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="79dfd-215">SQL sorgusu için belirtilen **sorgu** özelliği DBA verileri seçer. Veritabanındaki Siparişler tablosu.</span><span class="sxs-lookup"><span data-stu-id="79dfd-215">The SQL query specified for the **query** property selects the data from the DBA.Orders table in the database.</span></span>

```JSON
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from DBA.Orders"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "SybaseDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobSybaseDataSet"
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
                "name": "SybaseToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="79dfd-216">Sybase için tür eşlemesi</span><span class="sxs-lookup"><span data-stu-id="79dfd-216">Type mapping for Sybase</span></span>
<span data-ttu-id="79dfd-217">Bölümünde belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopya etkinliği aşağıdaki 2 adımlı yaklaşımı türleriyle havuz için kaynak türünden otomatik tür dönüşümleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="79dfd-217">As mentioned in the [Data Movement Activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="79dfd-218">Yerel kaynak türlerinden .NET türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="79dfd-218">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="79dfd-219">.NET türünden yerel havuz türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="79dfd-219">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="79dfd-220">Sybase T-SQL ve T-SQL türlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="79dfd-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="79dfd-221">Bir eşleme tablosu için sql türlerinden .NET türü için bkz: [Azure SQL Bağlayıcısı](data-factory-azure-sql-connector.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="79dfd-221">For a mapping table from sql types to .NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="79dfd-222">Kaynak havuzu sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="79dfd-222">Map source to sink columns</span></span>
<span data-ttu-id="79dfd-223">Havuz dataset sütunlara kaynak kümesindeki eşleme sütunları hakkında bilgi edinmek için [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="79dfd-223">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="79dfd-224">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="79dfd-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="79dfd-225">İlişkisel veri kopyalama verileri depoladığında, Yinelenebilirlik istenmeyen sonuçları önlemek için göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="79dfd-225">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="79dfd-226">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79dfd-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="79dfd-227">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79dfd-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="79dfd-228">Bir dilim iki yolla yeniden çalıştırıldığında, aynı veri dilimi çalıştırmak kaç kez geçtiğinden bağımsız okuduğunuzdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="79dfd-228">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="79dfd-229">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="79dfd-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="79dfd-230">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="79dfd-230">Performance and Tuning</span></span>
<span data-ttu-id="79dfd-231">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve onu en iyi duruma getirmek için çeşitli yollar etkisi performansını anahtar Etkenler hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="79dfd-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
