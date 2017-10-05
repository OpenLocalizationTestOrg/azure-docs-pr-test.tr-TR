---
title: "Azure Data Factory kullanarak MySQL'den veri taşıma | Microsoft Docs"
description: "Azure Data Factory kullanarak MySQL veritabanından veri taşıma hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 452f4fce-9eb5-40a0-92f8-1e98691bea4c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jingwang
ms.openlocfilehash: 05159bfd98977d0b57b43fbc02e4579439f7ce4c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="3b3f1-103">Veri öğesinden MySQL Azure Data Factory kullanarak Taşı</span><span class="sxs-lookup"><span data-stu-id="3b3f1-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="3b3f1-104">Bu makalede kopya etkinliği Azure Data Factory'de bir şirket içi MySQL veritabanından veri taşımak için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MySQL database.</span></span> <span data-ttu-id="3b3f1-105">Derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) kopyalama etkinliği ile veri taşıma için genel bir bakış sunar makalesi.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="3b3f1-106">Bir şirket içi MySQL veri deposundan verileri herhangi bir desteklenen havuz veri deposuna kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-106">You can copy data from an on-premises MySQL data store to any supported sink data store.</span></span> <span data-ttu-id="3b3f1-107">Veri depoları havuzlarını kopyalama etkinliği tarafından desteklenen bir listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="3b3f1-108">Veri Fabrikası şu anda yalnızca veri taşımayı MySQL veri deposundan diğer veri depolarına, ancak verileri diğer veri depolarına bir MySQL veri deposuna taşıma değil destekler.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-108">Data factory currently supports only moving data from a MySQL data store to other data stores, but not for moving data from other data stores to an MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3b3f1-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3b3f1-109">Prerequisites</span></span>
<span data-ttu-id="3b3f1-110">Data Factory hizmetinin şirket içi MySQL kaynaklarına veri yönetimi ağ geçidi kullanarak bağlanmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-110">Data Factory service supports connecting to on-premises MySQL sources using the Data Management Gateway.</span></span> <span data-ttu-id="3b3f1-111">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale veri yönetimi ağ geçidi ve ağ geçidi kurun ayarlama hakkında adım adım yönergeleri hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="3b3f1-112">Bir Azure Iaas sanal makine (VM) MySQL veritabanını barındıran olsa bile ağ geçidi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-112">Gateway is required even if the MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="3b3f1-113">Ağ geçidi veritabanına bağlanıp sürece veri deposu olarak aynı VM veya farklı bir VM ağ geçidi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-113">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="3b3f1-114">Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="3b3f1-115">Desteklenen sürümleri ve yükleme</span><span class="sxs-lookup"><span data-stu-id="3b3f1-115">Supported versions and installation</span></span>
<span data-ttu-id="3b3f1-116">Veri Yönetimi MySQL veritabanına bağlanmak ağ geçidi için yüklemeniz gerekir. [MySQL Connector/Net için Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (sürüm 6.6.5 veya üstü) aynı sistemde veri yönetimi ağ geçidi olarak.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-116">For Data Management Gateway to connect to the MySQL Database, you need to install the [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 or above) on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="3b3f1-117">MySQL sürüm 5.1 ve üzeri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-117">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> <span data-ttu-id="3b3f1-118">MySQL Connector/Net daha yüksek bir sürüme yükseltmek için "Uzak taraf aktarım akışı. kapatıldığı için kimlik doğrulaması başarısız oldu" hata isabet durumunda göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-118">If you hit error on "Authentication failed because the remote party has closed the transport stream.", consider to upgrade the MySQL Connector/Net to higher version.</span></span>

## <a name="getting-started"></a><span data-ttu-id="3b3f1-119">Başlarken</span><span class="sxs-lookup"><span data-stu-id="3b3f1-119">Getting started</span></span>
<span data-ttu-id="3b3f1-120">Farklı araçlar/API'lerini kullanarak bir şirket içi Cassandra veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-120">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="3b3f1-121">Bir işlem hattı oluşturmak için en kolay yolu kullanmaktır **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-121">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="3b3f1-122">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) veri kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="3b3f1-123">Bir işlem hattı oluşturmak için aşağıdaki araçları kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu**, **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-123">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="3b3f1-124">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="3b3f1-125">Araçlar ya da API'leri kullanıp bir havuz veri deposu için bir kaynak veri deposundan verileri taşır bir ardışık düzen oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3b3f1-125">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="3b3f1-126">Oluşturma **bağlantılı Hizmetleri** girdi ve çıktı verilerini bağlamak için veri fabrikanıza depolar.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-126">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="3b3f1-127">Oluşturma **veri kümeleri** kopyalama işlemi için girdi ve çıktı verilerini temsil etmek için.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-127">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="3b3f1-128">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="3b3f1-129">Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-129">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="3b3f1-130">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, JSON biçimini kullanarak bu Data Factory varlıklarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="3b3f1-131">Bir şirket içi MySQL veri deposundan verileri kopyalamak için kullanılan Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: veri kopyalama MySQL'den Azure Blob](#json-example-copy-data-from-mysql-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-131">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL to Azure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="3b3f1-132">Aşağıdaki bölümler, Data Factory varlıklarını belirli bir MySQL veri deposuna tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="3b3f1-132">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="3b3f1-133">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="3b3f1-133">Linked service properties</span></span>
<span data-ttu-id="3b3f1-134">Aşağıdaki tabloda, JSON öğeleri MySQL bağlantılı hizmete özgü açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-134">The following table provides description for JSON elements specific to MySQL linked service.</span></span>

| <span data-ttu-id="3b3f1-135">Özellik</span><span class="sxs-lookup"><span data-stu-id="3b3f1-135">Property</span></span> | <span data-ttu-id="3b3f1-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3b3f1-136">Description</span></span> | <span data-ttu-id="3b3f1-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3b3f1-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b3f1-138">type</span><span class="sxs-lookup"><span data-stu-id="3b3f1-138">type</span></span> |<span data-ttu-id="3b3f1-139">Type özelliği ayarlanmalıdır: **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="3b3f1-139">The type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="3b3f1-140">Evet</span><span class="sxs-lookup"><span data-stu-id="3b3f1-140">Yes</span></span> |
| <span data-ttu-id="3b3f1-141">sunucu</span><span class="sxs-lookup"><span data-stu-id="3b3f1-141">server</span></span> |<span data-ttu-id="3b3f1-142">MySQL sunucu adı.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-142">Name of the MySQL server.</span></span> |<span data-ttu-id="3b3f1-143">Evet</span><span class="sxs-lookup"><span data-stu-id="3b3f1-143">Yes</span></span> |
| <span data-ttu-id="3b3f1-144">Veritabanı</span><span class="sxs-lookup"><span data-stu-id="3b3f1-144">database</span></span> |<span data-ttu-id="3b3f1-145">MySQL veritabanının adı.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-145">Name of the MySQL database.</span></span> |<span data-ttu-id="3b3f1-146">Evet</span><span class="sxs-lookup"><span data-stu-id="3b3f1-146">Yes</span></span> |
| <span data-ttu-id="3b3f1-147">Şema</span><span class="sxs-lookup"><span data-stu-id="3b3f1-147">schema</span></span> |<span data-ttu-id="3b3f1-148">Veritabanı şemasında adı.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-148">Name of the schema in the database.</span></span> |<span data-ttu-id="3b3f1-149">Hayır</span><span class="sxs-lookup"><span data-stu-id="3b3f1-149">No</span></span> |
| <span data-ttu-id="3b3f1-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3b3f1-150">authenticationType</span></span> |<span data-ttu-id="3b3f1-151">MySQL veritabanına bağlanmak için kullanılan kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-151">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="3b3f1-152">Olası değerler şunlardır: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-152">Possible values are: `Basic`.</span></span> |<span data-ttu-id="3b3f1-153">Evet</span><span class="sxs-lookup"><span data-stu-id="3b3f1-153">Yes</span></span> |
| <span data-ttu-id="3b3f1-154">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="3b3f1-154">username</span></span> |<span data-ttu-id="3b3f1-155">MySQL veritabanına bağlanmak için kullanıcı adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-155">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="3b3f1-156">Evet</span><span class="sxs-lookup"><span data-stu-id="3b3f1-156">Yes</span></span> |
| <span data-ttu-id="3b3f1-157">password</span><span class="sxs-lookup"><span data-stu-id="3b3f1-157">password</span></span> |<span data-ttu-id="3b3f1-158">Belirttiğiniz kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-158">Specify password for the user account you specified.</span></span> |<span data-ttu-id="3b3f1-159">Evet</span><span class="sxs-lookup"><span data-stu-id="3b3f1-159">Yes</span></span> |
| <span data-ttu-id="3b3f1-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b3f1-160">gatewayName</span></span> |<span data-ttu-id="3b3f1-161">Data Factory hizmetinin şirket içi MySQL veritabanına bağlanmak için kullanması gereken ağ geçidinin adı.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-161">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="3b3f1-162">Evet</span><span class="sxs-lookup"><span data-stu-id="3b3f1-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="3b3f1-163">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="3b3f1-163">Dataset properties</span></span>
<span data-ttu-id="3b3f1-164">Bölümler & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="3b3f1-165">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="3b3f1-166">**TypeProperties** bölüm veri kümesi her tür için farklıdır ve verilerin veri deposunda konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="3b3f1-167">TypeProperties bölüm türü veri kümesi için **RelationalTable** (MySQL dataset içerir) aşağıdaki özelliklere sahip</span><span class="sxs-lookup"><span data-stu-id="3b3f1-167">The typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has the following properties</span></span>

| <span data-ttu-id="3b3f1-168">Özellik</span><span class="sxs-lookup"><span data-stu-id="3b3f1-168">Property</span></span> | <span data-ttu-id="3b3f1-169">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3b3f1-169">Description</span></span> | <span data-ttu-id="3b3f1-170">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3b3f1-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b3f1-171">tableName</span><span class="sxs-lookup"><span data-stu-id="3b3f1-171">tableName</span></span> |<span data-ttu-id="3b3f1-172">MySQL veritabanı örneğinde bağlantılı hizmet başvurduğu tablonun adı.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-172">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="3b3f1-173">Hayır (varsa **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="3b3f1-173">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="3b3f1-174">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="3b3f1-174">Copy activity properties</span></span>
<span data-ttu-id="3b3f1-175">Bölümler & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz: [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="3b3f1-176">Ad, açıklama, giriş ve çıkış tabloları gibi özellikleri olan ilkeleri etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-176">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="3b3f1-177">Bulunan özellikler **typeProperties** etkinlik bölümünü her etkinlik türü ile değişir.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-177">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="3b3f1-178">Kopya etkinliği için bunlar türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-178">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="3b3f1-179">Kopyalama etkinliği kaynağında türü olduğunda **RelationalSource** (içeren MySQL), aşağıdaki özellikler typeProperties bölümünde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="3b3f1-179">When source in copy activity is of type **RelationalSource** (which includes MySQL), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="3b3f1-180">Özellik</span><span class="sxs-lookup"><span data-stu-id="3b3f1-180">Property</span></span> | <span data-ttu-id="3b3f1-181">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3b3f1-181">Description</span></span> | <span data-ttu-id="3b3f1-182">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="3b3f1-182">Allowed values</span></span> | <span data-ttu-id="3b3f1-183">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3b3f1-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b3f1-184">sorgu</span><span class="sxs-lookup"><span data-stu-id="3b3f1-184">query</span></span> |<span data-ttu-id="3b3f1-185">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-185">Use the custom query to read data.</span></span> |<span data-ttu-id="3b3f1-186">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-186">SQL query string.</span></span> <span data-ttu-id="3b3f1-187">Örneğin: seçin * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-187">For example: select * from MyTable.</span></span> |<span data-ttu-id="3b3f1-188">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="3b3f1-188">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-to-azure-blob"></a><span data-ttu-id="3b3f1-189">JSON örnek: veri kopyalama MySQL'den Azure Blob</span><span class="sxs-lookup"><span data-stu-id="3b3f1-189">JSON example: Copy data from MySQL to Azure Blob</span></span>
<span data-ttu-id="3b3f1-190">Bu örnek kullanarak bir işlem hattı oluşturmak için kullanabileceğiniz örnek JSON tanımları sağlar, [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3b3f1-190">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="3b3f1-191">Bir Azure Blob depolama alanına bir şirket içi MySQL veritabanından veri kopyalamak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-191">It shows how to copy data from an on-premises MySQL database to an Azure Blob Storage.</span></span> <span data-ttu-id="3b3f1-192">Ancak, veri herhangi belirtildiği havuzlarını kopyalanabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kopya etkinliği Azure Data Factory kullanarak.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-192">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b3f1-193">Bu örnek, JSON parçacıklarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-193">This sample provides JSON snippets.</span></span> <span data-ttu-id="3b3f1-194">Data factory oluşturmak için adım adım yönergeler içermez.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-194">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="3b3f1-195">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-195">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="3b3f1-196">Örnek aşağıdaki data factory varlıklarını sahiptir:</span><span class="sxs-lookup"><span data-stu-id="3b3f1-196">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="3b3f1-197">Bağlı hizmet türü [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3b3f1-197">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="3b3f1-198">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3b3f1-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="3b3f1-199">Bir giriş [dataset](data-factory-create-datasets.md) türü [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3b3f1-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="3b3f1-200">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3b3f1-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="3b3f1-201">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="3b3f1-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="3b3f1-202">Örnek veriler MySQL veritabanında bir sorgu sonucu bir blobu saatlik kopyalar.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-202">The sample copies data from a query result in MySQL database to a blob hourly.</span></span> <span data-ttu-id="3b3f1-203">Bu örnekler kullanılan JSON özellikleri örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-203">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="3b3f1-204">İlk adım olarak, veri yönetimi ağ geçidi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-204">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="3b3f1-205">Yönergeler bulunan [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-205">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="3b3f1-206">**MySQL hizmeti bağlı:**</span><span class="sxs-lookup"><span data-stu-id="3b3f1-206">**MySQL linked service:**</span></span>

```JSON
    {
      "name": "OnPremMySqlLinkedService",
      "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
          "server": "<server name>",
          "database": "<database name>",
          "schema": "<schema name>",
          "authenticationType": "<authentication type>",
          "userName": "<user name>",
          "password": "<password>",
          "gatewayName": "<gateway>"
        }
      }
    }
```

<span data-ttu-id="3b3f1-207">**Azure Storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="3b3f1-207">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="3b3f1-208">**MySQL girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="3b3f1-208">**MySQL input dataset:**</span></span>

<span data-ttu-id="3b3f1-209">Örnek bir tablo "MyTable" MySQL içinde oluşturduğunuz ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-209">The sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="3b3f1-210">"Dış" ayarı: "true" bildirir Data Factory hizmetinin tablo data factory dış ve veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-210">Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
    {
        "name": "MySqlDataSet",
        "properties": {
            "published": false,
            "type": "RelationalTable",
            "linkedServiceName": "OnPremMySqlLinkedService",
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

<span data-ttu-id="3b3f1-211">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="3b3f1-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="3b3f1-212">Veri her saat yeni bir bloba yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="3b3f1-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="3b3f1-213">Blob klasör yolu dinamik işlenmekte olan dilim başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="3b3f1-214">Klasör yolu yıl, ay, gün ve saat bölümleri başlangıç saatini kullanır.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
    {
        "name": "AzureBlobMySqlDataSet",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "mycontainer/mysql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="3b3f1-215">**Kopyalama etkinliği ile kanal:**</span><span class="sxs-lookup"><span data-stu-id="3b3f1-215">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="3b3f1-216">Ardışık Düzen giriş ve çıkış veri kümeleri kullanmak üzere yapılandırıldığı ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-216">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="3b3f1-217">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **RelationalSource** ve **havuz** türü ayarlanmış **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="3b3f1-218">SQL sorgusu için belirtilen **sorgu** özelliği veri kopyalamak için son bir saat içindeki seçer.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```JSON
    {
        "name": "CopyMySqlToBlob",
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
                            "name": "MySqlDataSet"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobMySqlDataSet"
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
                    "name": "MySqlToBlob"
                }
            ],
            "start": "2014-06-01T18:00:00Z",
            "end": "2014-06-01T19:00:00Z"
        }
    }
```


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="3b3f1-219">Tür eşlemesi için MySQL</span><span class="sxs-lookup"><span data-stu-id="3b3f1-219">Type mapping for MySQL</span></span>
<span data-ttu-id="3b3f1-220">Bölümünde belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği, aşağıdaki iki aşamalı yaklaşımı türleriyle havuz için kaynak türünden otomatik tür dönüşümleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="3b3f1-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="3b3f1-221">Yerel kaynak türlerinden .NET türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="3b3f1-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="3b3f1-222">.NET türünden yerel havuz türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="3b3f1-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="3b3f1-223">MySQL için veri taşırken, aşağıdaki eşlemelerini MySQL türlerinden .NET türleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-223">When moving data to MySQL, the following mappings are used from MySQL types to .NET types.</span></span>

| <span data-ttu-id="3b3f1-224">MySQL veritabanı türü</span><span class="sxs-lookup"><span data-stu-id="3b3f1-224">MySQL Database type</span></span> | <span data-ttu-id="3b3f1-225">.NET framework türü</span><span class="sxs-lookup"><span data-stu-id="3b3f1-225">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="3b3f1-226">bigint imzalanmamış</span><span class="sxs-lookup"><span data-stu-id="3b3f1-226">bigint unsigned</span></span> |<span data-ttu-id="3b3f1-227">Ondalık</span><span class="sxs-lookup"><span data-stu-id="3b3f1-227">Decimal</span></span> |
| <span data-ttu-id="3b3f1-228">bigint</span><span class="sxs-lookup"><span data-stu-id="3b3f1-228">bigint</span></span> |<span data-ttu-id="3b3f1-229">Int64</span><span class="sxs-lookup"><span data-stu-id="3b3f1-229">Int64</span></span> |
| <span data-ttu-id="3b3f1-230">bit</span><span class="sxs-lookup"><span data-stu-id="3b3f1-230">bit</span></span> |<span data-ttu-id="3b3f1-231">Ondalık</span><span class="sxs-lookup"><span data-stu-id="3b3f1-231">Decimal</span></span> |
| <span data-ttu-id="3b3f1-232">BLOB</span><span class="sxs-lookup"><span data-stu-id="3b3f1-232">blob</span></span> |<span data-ttu-id="3b3f1-233">Byte]</span><span class="sxs-lookup"><span data-stu-id="3b3f1-233">Byte[]</span></span> |
| <span data-ttu-id="3b3f1-234">bool</span><span class="sxs-lookup"><span data-stu-id="3b3f1-234">bool</span></span> |<span data-ttu-id="3b3f1-235">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="3b3f1-235">Boolean</span></span> |
| <span data-ttu-id="3b3f1-236">char</span><span class="sxs-lookup"><span data-stu-id="3b3f1-236">char</span></span> |<span data-ttu-id="3b3f1-237">Dize</span><span class="sxs-lookup"><span data-stu-id="3b3f1-237">String</span></span> |
| <span data-ttu-id="3b3f1-238">Tarih</span><span class="sxs-lookup"><span data-stu-id="3b3f1-238">date</span></span> |<span data-ttu-id="3b3f1-239">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="3b3f1-239">Datetime</span></span> |
| <span data-ttu-id="3b3f1-240">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="3b3f1-240">datetime</span></span> |<span data-ttu-id="3b3f1-241">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="3b3f1-241">Datetime</span></span> |
| <span data-ttu-id="3b3f1-242">Ondalık</span><span class="sxs-lookup"><span data-stu-id="3b3f1-242">decimal</span></span> |<span data-ttu-id="3b3f1-243">Ondalık</span><span class="sxs-lookup"><span data-stu-id="3b3f1-243">Decimal</span></span> |
| <span data-ttu-id="3b3f1-244">çift duyarlıklı</span><span class="sxs-lookup"><span data-stu-id="3b3f1-244">double precision</span></span> |<span data-ttu-id="3b3f1-245">Çift</span><span class="sxs-lookup"><span data-stu-id="3b3f1-245">Double</span></span> |
| <span data-ttu-id="3b3f1-246">Çift</span><span class="sxs-lookup"><span data-stu-id="3b3f1-246">double</span></span> |<span data-ttu-id="3b3f1-247">Çift</span><span class="sxs-lookup"><span data-stu-id="3b3f1-247">Double</span></span> |
| <span data-ttu-id="3b3f1-248">Enum</span><span class="sxs-lookup"><span data-stu-id="3b3f1-248">enum</span></span> |<span data-ttu-id="3b3f1-249">Dize</span><span class="sxs-lookup"><span data-stu-id="3b3f1-249">String</span></span> |
| <span data-ttu-id="3b3f1-250">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="3b3f1-250">float</span></span> |<span data-ttu-id="3b3f1-251">Tek</span><span class="sxs-lookup"><span data-stu-id="3b3f1-251">Single</span></span> |
| <span data-ttu-id="3b3f1-252">İmzasız int</span><span class="sxs-lookup"><span data-stu-id="3b3f1-252">int unsigned</span></span> |<span data-ttu-id="3b3f1-253">Int64</span><span class="sxs-lookup"><span data-stu-id="3b3f1-253">Int64</span></span> |
| <span data-ttu-id="3b3f1-254">Int</span><span class="sxs-lookup"><span data-stu-id="3b3f1-254">int</span></span> |<span data-ttu-id="3b3f1-255">Int32</span><span class="sxs-lookup"><span data-stu-id="3b3f1-255">Int32</span></span> |
| <span data-ttu-id="3b3f1-256">işaretsiz tamsayı</span><span class="sxs-lookup"><span data-stu-id="3b3f1-256">integer unsigned</span></span> |<span data-ttu-id="3b3f1-257">Int64</span><span class="sxs-lookup"><span data-stu-id="3b3f1-257">Int64</span></span> |
| <span data-ttu-id="3b3f1-258">tamsayı</span><span class="sxs-lookup"><span data-stu-id="3b3f1-258">integer</span></span> |<span data-ttu-id="3b3f1-259">Int32</span><span class="sxs-lookup"><span data-stu-id="3b3f1-259">Int32</span></span> |
| <span data-ttu-id="3b3f1-260">uzun varbinary</span><span class="sxs-lookup"><span data-stu-id="3b3f1-260">long varbinary</span></span> |<span data-ttu-id="3b3f1-261">Byte]</span><span class="sxs-lookup"><span data-stu-id="3b3f1-261">Byte[]</span></span> |
| <span data-ttu-id="3b3f1-262">uzun varchar</span><span class="sxs-lookup"><span data-stu-id="3b3f1-262">long varchar</span></span> |<span data-ttu-id="3b3f1-263">Dize</span><span class="sxs-lookup"><span data-stu-id="3b3f1-263">String</span></span> |
| <span data-ttu-id="3b3f1-264">longblob</span><span class="sxs-lookup"><span data-stu-id="3b3f1-264">longblob</span></span> |<span data-ttu-id="3b3f1-265">Byte]</span><span class="sxs-lookup"><span data-stu-id="3b3f1-265">Byte[]</span></span> |
| <span data-ttu-id="3b3f1-266">LONGTEXT</span><span class="sxs-lookup"><span data-stu-id="3b3f1-266">longtext</span></span> |<span data-ttu-id="3b3f1-267">Dize</span><span class="sxs-lookup"><span data-stu-id="3b3f1-267">String</span></span> |
| <span data-ttu-id="3b3f1-268">mediumblob</span><span class="sxs-lookup"><span data-stu-id="3b3f1-268">mediumblob</span></span> |<span data-ttu-id="3b3f1-269">Byte]</span><span class="sxs-lookup"><span data-stu-id="3b3f1-269">Byte[]</span></span> |
| <span data-ttu-id="3b3f1-270">İmzasız mediumint</span><span class="sxs-lookup"><span data-stu-id="3b3f1-270">mediumint unsigned</span></span> |<span data-ttu-id="3b3f1-271">Int64</span><span class="sxs-lookup"><span data-stu-id="3b3f1-271">Int64</span></span> |
| <span data-ttu-id="3b3f1-272">mediumint</span><span class="sxs-lookup"><span data-stu-id="3b3f1-272">mediumint</span></span> |<span data-ttu-id="3b3f1-273">Int32</span><span class="sxs-lookup"><span data-stu-id="3b3f1-273">Int32</span></span> |
| <span data-ttu-id="3b3f1-274">mediumtext</span><span class="sxs-lookup"><span data-stu-id="3b3f1-274">mediumtext</span></span> |<span data-ttu-id="3b3f1-275">Dize</span><span class="sxs-lookup"><span data-stu-id="3b3f1-275">String</span></span> |
| <span data-ttu-id="3b3f1-276">sayısal</span><span class="sxs-lookup"><span data-stu-id="3b3f1-276">numeric</span></span> |<span data-ttu-id="3b3f1-277">Ondalık</span><span class="sxs-lookup"><span data-stu-id="3b3f1-277">Decimal</span></span> |
| <span data-ttu-id="3b3f1-278">Gerçek</span><span class="sxs-lookup"><span data-stu-id="3b3f1-278">real</span></span> |<span data-ttu-id="3b3f1-279">Çift</span><span class="sxs-lookup"><span data-stu-id="3b3f1-279">Double</span></span> |
| <span data-ttu-id="3b3f1-280">ayarlama</span><span class="sxs-lookup"><span data-stu-id="3b3f1-280">set</span></span> |<span data-ttu-id="3b3f1-281">Dize</span><span class="sxs-lookup"><span data-stu-id="3b3f1-281">String</span></span> |
| <span data-ttu-id="3b3f1-282">işaretsiz tamsayı</span><span class="sxs-lookup"><span data-stu-id="3b3f1-282">smallint unsigned</span></span> |<span data-ttu-id="3b3f1-283">Int32</span><span class="sxs-lookup"><span data-stu-id="3b3f1-283">Int32</span></span> |
| <span data-ttu-id="3b3f1-284">tamsayı</span><span class="sxs-lookup"><span data-stu-id="3b3f1-284">smallint</span></span> |<span data-ttu-id="3b3f1-285">Int16</span><span class="sxs-lookup"><span data-stu-id="3b3f1-285">Int16</span></span> |
| <span data-ttu-id="3b3f1-286">Metin</span><span class="sxs-lookup"><span data-stu-id="3b3f1-286">text</span></span> |<span data-ttu-id="3b3f1-287">Dize</span><span class="sxs-lookup"><span data-stu-id="3b3f1-287">String</span></span> |
| <span data-ttu-id="3b3f1-288">time</span><span class="sxs-lookup"><span data-stu-id="3b3f1-288">time</span></span> |<span data-ttu-id="3b3f1-289">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3b3f1-289">TimeSpan</span></span> |
| <span data-ttu-id="3b3f1-290">timestamp</span><span class="sxs-lookup"><span data-stu-id="3b3f1-290">timestamp</span></span> |<span data-ttu-id="3b3f1-291">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="3b3f1-291">Datetime</span></span> |
| <span data-ttu-id="3b3f1-292">tinyblob</span><span class="sxs-lookup"><span data-stu-id="3b3f1-292">tinyblob</span></span> |<span data-ttu-id="3b3f1-293">Byte]</span><span class="sxs-lookup"><span data-stu-id="3b3f1-293">Byte[]</span></span> |
| <span data-ttu-id="3b3f1-294">İmzasız tinyint</span><span class="sxs-lookup"><span data-stu-id="3b3f1-294">tinyint unsigned</span></span> |<span data-ttu-id="3b3f1-295">Int16</span><span class="sxs-lookup"><span data-stu-id="3b3f1-295">Int16</span></span> |
| <span data-ttu-id="3b3f1-296">Mini tamsayı</span><span class="sxs-lookup"><span data-stu-id="3b3f1-296">tinyint</span></span> |<span data-ttu-id="3b3f1-297">Int16</span><span class="sxs-lookup"><span data-stu-id="3b3f1-297">Int16</span></span> |
| <span data-ttu-id="3b3f1-298">tinytext</span><span class="sxs-lookup"><span data-stu-id="3b3f1-298">tinytext</span></span> |<span data-ttu-id="3b3f1-299">Dize</span><span class="sxs-lookup"><span data-stu-id="3b3f1-299">String</span></span> |
| <span data-ttu-id="3b3f1-300">varchar</span><span class="sxs-lookup"><span data-stu-id="3b3f1-300">varchar</span></span> |<span data-ttu-id="3b3f1-301">Dize</span><span class="sxs-lookup"><span data-stu-id="3b3f1-301">String</span></span> |
| <span data-ttu-id="3b3f1-302">Yıl</span><span class="sxs-lookup"><span data-stu-id="3b3f1-302">year</span></span> |<span data-ttu-id="3b3f1-303">Int</span><span class="sxs-lookup"><span data-stu-id="3b3f1-303">Int</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="3b3f1-304">Kaynak havuzu sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="3b3f1-304">Map source to sink columns</span></span>
<span data-ttu-id="3b3f1-305">Havuz dataset sütunlara kaynak kümesindeki eşleme sütunları hakkında bilgi edinmek için [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="3b3f1-305">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="3b3f1-306">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="3b3f1-306">Repeatable read from relational sources</span></span>
<span data-ttu-id="3b3f1-307">İlişkisel veri kopyalama verileri depoladığında, Yinelenebilirlik istenmeyen sonuçları önlemek için göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-307">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="3b3f1-308">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-308">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="3b3f1-309">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-309">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="3b3f1-310">Bir dilim iki yolla yeniden çalıştırıldığında, aynı veri dilimi çalıştırmak kaç kez geçtiğinden bağımsız okuduğunuzdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-310">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="3b3f1-311">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="3b3f1-311">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="3b3f1-312">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="3b3f1-312">Performance and Tuning</span></span>
<span data-ttu-id="3b3f1-313">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve onu en iyi duruma getirmek için çeşitli yollar etkisi performansını anahtar Etkenler hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="3b3f1-313">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
