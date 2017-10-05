---
title: "Data Factory kullanarak Cassandra veri taşıma | Microsoft Docs"
description: "Azure Data Factory kullanarak bir şirket içi Cassandra veritabanından veri taşıma hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: f2b225bdbdf2880d26a6ab5f992301bf0a804b0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a><span data-ttu-id="6ca55-103">Azure Data Factory kullanarak bir şirket içi Cassandra veritabanından veri taşıma</span><span class="sxs-lookup"><span data-stu-id="6ca55-103">Move data from an on-premises Cassandra database using Azure Data Factory</span></span>
<span data-ttu-id="6ca55-104">Bu makalede kopya etkinliği Azure Data Factory'de bir şirket içi Cassandra veritabanından veri taşımak için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6ca55-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Cassandra database.</span></span> <span data-ttu-id="6ca55-105">Derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) kopyalama etkinliği ile veri taşıma için genel bir bakış sunar makalesi.</span><span class="sxs-lookup"><span data-stu-id="6ca55-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="6ca55-106">Bir şirket içi Cassandra veri deposundan verileri herhangi bir desteklenen havuz veri deposuna kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ca55-106">You can copy data from an on-premises Cassandra data store to any supported sink data store.</span></span> <span data-ttu-id="6ca55-107">Veri depoları havuzlarını kopyalama etkinliği tarafından desteklenen bir listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="6ca55-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="6ca55-108">Veri Fabrikası şu anda yalnızca veri taşımayı Cassandra veri deposundan diğer veri depolarına, ancak verileri diğer veri depolarına Cassandra veri deposuna taşıma değil destekler.</span><span class="sxs-lookup"><span data-stu-id="6ca55-108">Data factory currently supports only moving data from a Cassandra data store to other data stores, but not for moving data from other data stores to a Cassandra data store.</span></span> 

## <a name="supported-versions"></a><span data-ttu-id="6ca55-109">Desteklenen sürümler</span><span class="sxs-lookup"><span data-stu-id="6ca55-109">Supported versions</span></span>
<span data-ttu-id="6ca55-110">Cassandra bağlayıcı Cassandra aşağıdaki sürümlerini destekler: 2.X.</span><span class="sxs-lookup"><span data-stu-id="6ca55-110">The Cassandra connector supports the following versions of Cassandra: 2.X.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ca55-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6ca55-111">Prerequisites</span></span>
<span data-ttu-id="6ca55-112">Azure Data Factory hizmetinin şirket içi Cassandra veritabanınıza bağlanmak veritabanını barındıran aynı makine üzerindeki veya veritabanı ile kaynakları için rekabete önlemek için ayrı bir makine veri yönetimi ağ geçidi yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ca55-112">For the Azure Data Factory service to be able to connect to your on-premises Cassandra database, you must install a Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span></span> <span data-ttu-id="6ca55-113">Veri Yönetimi ağ geçidi, şirket içi veri kaynakları bulut hizmetlerine güvenli ve yönetilen bir şekilde birbirine bağlayan bir bileşenidir.</span><span class="sxs-lookup"><span data-stu-id="6ca55-113">Data Management Gateway is a component that connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="6ca55-114">Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) makale veri yönetimi ağ geçidi hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="6ca55-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="6ca55-115">Bkz: [buluta şirket içinden veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale verileri taşımak veri ardışık ağ geçidi kurun ayarı ilişkin adım adım yönergeler.</span><span class="sxs-lookup"><span data-stu-id="6ca55-115">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="6ca55-116">Veritabanı bulutta, örneğin, bir Azure Iaas sanal bile barındırılıyorsa Cassandra veritabanına bağlanmak için ağ geçidi kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ca55-116">You must use the gateway to connect to a Cassandra database even if the database is hosted in the cloud, for example, on an Azure IaaS VM.</span></span> <span data-ttu-id="6ca55-117">Y, veritabanını barındıran aynı VM ağ geçidi olabilir veya ağ geçidi olarak uzunluğunda ayrı bir VM'de veritabanına bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ca55-117">Y You can have the gateway on the same VM that hosts the database or on a separate VM as long as the gateway can connect to the database.</span></span>  

<span data-ttu-id="6ca55-118">Ağ geçidi yüklediğinizde, Cassandra veritabanına bağlanmak için kullanılan bir Microsoft Cassandra ODBC sürücüsü otomatik olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="6ca55-118">When you install the gateway, it automatically installs a Microsoft Cassandra ODBC driver used to connect to Cassandra database.</span></span> <span data-ttu-id="6ca55-119">Bu nedenle, Cassandra veritabanından veri kopyalama işlemi sırasında herhangi bir sürücüsü ağ geçidi makinesi üzerinde el ile yüklemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6ca55-119">Therefore, you don't need to manually install any driver on the gateway machine when copying data from the Cassandra database.</span></span> 

> [!NOTE]
> <span data-ttu-id="6ca55-120">Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="6ca55-120">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="6ca55-121">Başlarken</span><span class="sxs-lookup"><span data-stu-id="6ca55-121">Getting started</span></span>
<span data-ttu-id="6ca55-122">Farklı araçlar/API'lerini kullanarak bir şirket içi Cassandra veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6ca55-122">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="6ca55-123">Bir işlem hattı oluşturmak için en kolay yolu kullanmaktır **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="6ca55-123">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="6ca55-124">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) veri kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="6ca55-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="6ca55-125">Bir işlem hattı oluşturmak için aşağıdaki araçları kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu**, **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="6ca55-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6ca55-126">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="6ca55-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="6ca55-127">Araçlar ya da API'leri kullanıp bir havuz veri deposu için bir kaynak veri deposundan verileri taşır bir ardışık düzen oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6ca55-127">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="6ca55-128">Oluşturma **bağlantılı Hizmetleri** girdi ve çıktı verilerini bağlamak için veri fabrikanıza depolar.</span><span class="sxs-lookup"><span data-stu-id="6ca55-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="6ca55-129">Oluşturma **veri kümeleri** kopyalama işlemi için girdi ve çıktı verilerini temsil etmek için.</span><span class="sxs-lookup"><span data-stu-id="6ca55-129">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="6ca55-130">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="6ca55-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="6ca55-131">Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6ca55-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="6ca55-132">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, JSON biçimini kullanarak bu Data Factory varlıklarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="6ca55-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="6ca55-133">Bir şirket içi Cassandra veri deposundan verileri kopyalamak için kullanılan Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: veri kopyalama Cassandra Azure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="6ca55-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra to Azure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="6ca55-134">Aşağıdaki bölümler, Data Factory varlıklarını belirli bir Cassandra veri deposuna tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="6ca55-134">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Cassandra data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="6ca55-135">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="6ca55-135">Linked service properties</span></span>
<span data-ttu-id="6ca55-136">Aşağıdaki tabloda, JSON öğeleri Cassandra bağlantılı hizmete özgü açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ca55-136">The following table provides description for JSON elements specific to Cassandra linked service.</span></span>

| <span data-ttu-id="6ca55-137">Özellik</span><span class="sxs-lookup"><span data-stu-id="6ca55-137">Property</span></span> | <span data-ttu-id="6ca55-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6ca55-138">Description</span></span> | <span data-ttu-id="6ca55-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6ca55-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ca55-140">type</span><span class="sxs-lookup"><span data-stu-id="6ca55-140">type</span></span> |<span data-ttu-id="6ca55-141">Type özelliği ayarlanmalıdır: **OnPremisesCassandra**</span><span class="sxs-lookup"><span data-stu-id="6ca55-141">The type property must be set to: **OnPremisesCassandra**</span></span> |<span data-ttu-id="6ca55-142">Evet</span><span class="sxs-lookup"><span data-stu-id="6ca55-142">Yes</span></span> |
| <span data-ttu-id="6ca55-143">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="6ca55-143">host</span></span> |<span data-ttu-id="6ca55-144">Bir veya daha fazla IP adresleri veya ana bilgisayar adlarını Cassandra sunucuları.</span><span class="sxs-lookup"><span data-stu-id="6ca55-144">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="6ca55-145">IP adreslerini veya aynı anda tüm sunucularına bağlanmak için ana bilgisayar adlarını virgülle ayrılmış listesini belirtin.</span><span class="sxs-lookup"><span data-stu-id="6ca55-145">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="6ca55-146">Evet</span><span class="sxs-lookup"><span data-stu-id="6ca55-146">Yes</span></span> |
| <span data-ttu-id="6ca55-147">port</span><span class="sxs-lookup"><span data-stu-id="6ca55-147">port</span></span> |<span data-ttu-id="6ca55-148">İstemci bağlantılarını dinlemek için Cassandra sunucusunun kullandığı TCP bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="6ca55-148">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="6ca55-149">Hayır, varsayılan değer: 9042</span><span class="sxs-lookup"><span data-stu-id="6ca55-149">No, default value: 9042</span></span> |
| <span data-ttu-id="6ca55-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6ca55-150">authenticationType</span></span> |<span data-ttu-id="6ca55-151">Basic veya Anonymous</span><span class="sxs-lookup"><span data-stu-id="6ca55-151">Basic, or Anonymous</span></span> |<span data-ttu-id="6ca55-152">Evet</span><span class="sxs-lookup"><span data-stu-id="6ca55-152">Yes</span></span> |
| <span data-ttu-id="6ca55-153">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="6ca55-153">username</span></span> |<span data-ttu-id="6ca55-154">Kullanıcı hesabının kullanıcı adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="6ca55-154">Specify user name for the user account.</span></span> |<span data-ttu-id="6ca55-155">Evet, authenticationType temel olarak ayarlanmışsa.</span><span class="sxs-lookup"><span data-stu-id="6ca55-155">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="6ca55-156">password</span><span class="sxs-lookup"><span data-stu-id="6ca55-156">password</span></span> |<span data-ttu-id="6ca55-157">Kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="6ca55-157">Specify password for the user account.</span></span> |<span data-ttu-id="6ca55-158">Evet, authenticationType temel olarak ayarlanmışsa.</span><span class="sxs-lookup"><span data-stu-id="6ca55-158">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="6ca55-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6ca55-159">gatewayName</span></span> |<span data-ttu-id="6ca55-160">Şirket içi Cassandra veritabanına bağlanmak için kullanılan ağ geçidi adı.</span><span class="sxs-lookup"><span data-stu-id="6ca55-160">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="6ca55-161">Evet</span><span class="sxs-lookup"><span data-stu-id="6ca55-161">Yes</span></span> |
| <span data-ttu-id="6ca55-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="6ca55-162">encryptedCredential</span></span> |<span data-ttu-id="6ca55-163">Ağ Geçidi tarafından şifrelenmiş kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="6ca55-163">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="6ca55-164">Hayır</span><span class="sxs-lookup"><span data-stu-id="6ca55-164">No</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="6ca55-165">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="6ca55-165">Dataset properties</span></span>
<span data-ttu-id="6ca55-166">Bölümler & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="6ca55-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="6ca55-167">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="6ca55-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="6ca55-168">**TypeProperties** bölüm veri kümesi her tür için farklıdır ve verilerin veri deposunda konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ca55-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="6ca55-169">TypeProperties bölüm türü veri kümesi için **CassandraTable** aşağıdaki özelliklere sahip</span><span class="sxs-lookup"><span data-stu-id="6ca55-169">The typeProperties section for dataset of type **CassandraTable** has the following properties</span></span>

| <span data-ttu-id="6ca55-170">Özellik</span><span class="sxs-lookup"><span data-stu-id="6ca55-170">Property</span></span> | <span data-ttu-id="6ca55-171">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6ca55-171">Description</span></span> | <span data-ttu-id="6ca55-172">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6ca55-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ca55-173">keyspace</span><span class="sxs-lookup"><span data-stu-id="6ca55-173">keyspace</span></span> |<span data-ttu-id="6ca55-174">Keyspace veya Cassandra veritabanındaki şema adı.</span><span class="sxs-lookup"><span data-stu-id="6ca55-174">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="6ca55-175">Evet (varsa **sorgu** için **CassandraSource** tanımlı değil).</span><span class="sxs-lookup"><span data-stu-id="6ca55-175">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="6ca55-176">tableName</span><span class="sxs-lookup"><span data-stu-id="6ca55-176">tableName</span></span> |<span data-ttu-id="6ca55-177">Cassandra veritabanı tablosunun adı.</span><span class="sxs-lookup"><span data-stu-id="6ca55-177">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="6ca55-178">Evet (varsa **sorgu** için **CassandraSource** tanımlı değil).</span><span class="sxs-lookup"><span data-stu-id="6ca55-178">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="6ca55-179">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="6ca55-179">Copy activity properties</span></span>
<span data-ttu-id="6ca55-180">Bölümler & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz: [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="6ca55-180">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6ca55-181">Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6ca55-181">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="6ca55-182">Oysa etkinliğin typeProperties bölümündeki özellikler her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="6ca55-182">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="6ca55-183">Kopya etkinliği için bunlar türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="6ca55-183">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="6ca55-184">Kaynak türü olduğunda **CassandraSource**, typeProperties bölümünde aşağıdaki özellikler kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="6ca55-184">When source is of type **CassandraSource**, the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="6ca55-185">Özellik</span><span class="sxs-lookup"><span data-stu-id="6ca55-185">Property</span></span> | <span data-ttu-id="6ca55-186">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6ca55-186">Description</span></span> | <span data-ttu-id="6ca55-187">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="6ca55-187">Allowed values</span></span> | <span data-ttu-id="6ca55-188">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6ca55-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6ca55-189">sorgu</span><span class="sxs-lookup"><span data-stu-id="6ca55-189">query</span></span> |<span data-ttu-id="6ca55-190">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="6ca55-190">Use the custom query to read data.</span></span> |<span data-ttu-id="6ca55-191">SQL-92 sorgusu veya CQL sorgusu.</span><span class="sxs-lookup"><span data-stu-id="6ca55-191">SQL-92 query or CQL query.</span></span> <span data-ttu-id="6ca55-192">Bkz: [CQL başvuru](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="6ca55-192">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="6ca55-193">SQL sorgusu kullanırken belirtin **keyspace name.table adı** sorgulamak istediğiniz tabloyu temsil etmek için.</span><span class="sxs-lookup"><span data-stu-id="6ca55-193">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="6ca55-194">Hayır (tableName ve veri kümesi üzerinde keyspace tanımlanmışsa).</span><span class="sxs-lookup"><span data-stu-id="6ca55-194">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="6ca55-195">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="6ca55-195">consistencyLevel</span></span> |<span data-ttu-id="6ca55-196">Tutarlılık düzeyi kaç çoğaltmaları Okuma isteği için veri istemci uygulamasına geri dönmeden önce yanıt vermesi gereken belirtir.</span><span class="sxs-lookup"><span data-stu-id="6ca55-196">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="6ca55-197">Cassandra Okuma isteği karşılamak veriler için çoğaltmaları belirtilen sayısını denetler.</span><span class="sxs-lookup"><span data-stu-id="6ca55-197">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="6ca55-198">BİR, İKİ, ÜÇ, ÇEKİRDEK, TÜMÜ, LOCAL_QUORUM EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="6ca55-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="6ca55-199">Bkz: [veri tutarlılığını yapılandırma](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="6ca55-199">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="6ca55-200">Hayır.</span><span class="sxs-lookup"><span data-stu-id="6ca55-200">No.</span></span> <span data-ttu-id="6ca55-201">Varsayılan değer biridir.</span><span class="sxs-lookup"><span data-stu-id="6ca55-201">Default value is ONE.</span></span> |

## <a name="json-example-copy-data-from-cassandra-to-azure-blob"></a><span data-ttu-id="6ca55-202">JSON örnek: veri kopyalama Cassandra Azure Blob</span><span class="sxs-lookup"><span data-stu-id="6ca55-202">JSON example: Copy data from Cassandra to Azure Blob</span></span>
<span data-ttu-id="6ca55-203">Bu örnek kullanarak bir işlem hattı oluşturmak için kullanabileceğiniz örnek JSON tanımları sağlar, [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6ca55-203">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="6ca55-204">Bir Azure Blob depolama alanına bir şirket içi Cassandra veritabanından veri kopyalamak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="6ca55-204">It shows how to copy data from an on-premises Cassandra database to an Azure Blob Storage.</span></span> <span data-ttu-id="6ca55-205">Ancak, veri herhangi belirtildiği havuzlarını kopyalanabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kopya etkinliği Azure Data Factory kullanarak.</span><span class="sxs-lookup"><span data-stu-id="6ca55-205">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ca55-206">Bu örnek, JSON parçacıklarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ca55-206">This sample provides JSON snippets.</span></span> <span data-ttu-id="6ca55-207">Data factory oluşturmak için adım adım yönergeler içermez.</span><span class="sxs-lookup"><span data-stu-id="6ca55-207">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="6ca55-208">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="6ca55-208">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="6ca55-209">Örnek aşağıdaki data factory varlıklarını sahiptir:</span><span class="sxs-lookup"><span data-stu-id="6ca55-209">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="6ca55-210">Bağlı hizmet türü [OnPremisesCassandra](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6ca55-210">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span></span>
* <span data-ttu-id="6ca55-211">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6ca55-211">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="6ca55-212">Bir giriş [dataset](data-factory-create-datasets.md) türü [CassandraTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6ca55-212">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span></span>
* <span data-ttu-id="6ca55-213">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6ca55-213">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="6ca55-214">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [CassandraSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6ca55-214">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="6ca55-215">**Bağlantılı Cassandra hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="6ca55-215">**Cassandra linked service:**</span></span>

<span data-ttu-id="6ca55-216">Bu örnekte **Cassandra** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="6ca55-216">This example uses the **Cassandra** linked service.</span></span> <span data-ttu-id="6ca55-217">Bkz: [Cassandra bağlantılı hizmeti](#linked-service-properties) bu bağlantılı hizmet tarafından desteklenen özellikler bölümü.</span><span class="sxs-lookup"><span data-stu-id="6ca55-217">See [Cassandra linked service](#linked-service-properties) section for the properties supported by this linked service.</span></span>  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="6ca55-218">**Azure Storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="6ca55-218">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="6ca55-219">**Cassandra girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="6ca55-219">**Cassandra input dataset:**</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
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

<span data-ttu-id="6ca55-220">Ayarı **dış** için **true** Data Factory hizmetinin veri kümesi data factory dış ve veri fabrikasında bir etkinlik tarafından üretilen değil bildirir.</span><span class="sxs-lookup"><span data-stu-id="6ca55-220">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="6ca55-221">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="6ca55-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="6ca55-222">Veri her saat yeni bir bloba yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="6ca55-222">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="6ca55-223">**Etkinlik Cassandra kaynak ve Blob havuz sahip işlem hattı kopyalayın:**</span><span class="sxs-lookup"><span data-stu-id="6ca55-223">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span></span>

<span data-ttu-id="6ca55-224">Ardışık Düzen giriş ve çıkış veri kümeleri kullanmak üzere yapılandırıldığı ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="6ca55-224">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="6ca55-225">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **CassandraSource** ve **havuz** türü ayarlanmış **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="6ca55-225">In the pipeline JSON definition, the **source** type is set to **CassandraSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="6ca55-226">Bkz: [RelationalSource türü özellikleri](#copy-activity-properties) RelationalSource tarafından desteklenen özelliklerin listesi için.</span><span class="sxs-lookup"><span data-stu-id="6ca55-226">See [RelationalSource type properties](#copy-activity-properties) for the list of properties supported by the RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra to an Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"

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

### <a name="type-mapping-for-cassandra"></a><span data-ttu-id="6ca55-227">Tür eşlemesi için Cassandra</span><span class="sxs-lookup"><span data-stu-id="6ca55-227">Type mapping for Cassandra</span></span>
| <span data-ttu-id="6ca55-228">Cassandra türü</span><span class="sxs-lookup"><span data-stu-id="6ca55-228">Cassandra Type</span></span> | <span data-ttu-id="6ca55-229">.NET türü temelinde</span><span class="sxs-lookup"><span data-stu-id="6ca55-229">.Net Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="6ca55-230">ASCII</span><span class="sxs-lookup"><span data-stu-id="6ca55-230">ASCII</span></span> |<span data-ttu-id="6ca55-231">Dize</span><span class="sxs-lookup"><span data-stu-id="6ca55-231">String</span></span> |
| <span data-ttu-id="6ca55-232">BIGINT</span><span class="sxs-lookup"><span data-stu-id="6ca55-232">BIGINT</span></span> |<span data-ttu-id="6ca55-233">Int64</span><span class="sxs-lookup"><span data-stu-id="6ca55-233">Int64</span></span> |
| <span data-ttu-id="6ca55-234">BLOB</span><span class="sxs-lookup"><span data-stu-id="6ca55-234">BLOB</span></span> |<span data-ttu-id="6ca55-235">Byte]</span><span class="sxs-lookup"><span data-stu-id="6ca55-235">Byte[]</span></span> |
| <span data-ttu-id="6ca55-236">BOOLE DEĞERİ</span><span class="sxs-lookup"><span data-stu-id="6ca55-236">BOOLEAN</span></span> |<span data-ttu-id="6ca55-237">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="6ca55-237">Boolean</span></span> |
| <span data-ttu-id="6ca55-238">ONDALIK</span><span class="sxs-lookup"><span data-stu-id="6ca55-238">DECIMAL</span></span> |<span data-ttu-id="6ca55-239">Ondalık</span><span class="sxs-lookup"><span data-stu-id="6ca55-239">Decimal</span></span> |
| <span data-ttu-id="6ca55-240">ÇİFT</span><span class="sxs-lookup"><span data-stu-id="6ca55-240">DOUBLE</span></span> |<span data-ttu-id="6ca55-241">Çift</span><span class="sxs-lookup"><span data-stu-id="6ca55-241">Double</span></span> |
| <span data-ttu-id="6ca55-242">KAYAN NOKTA</span><span class="sxs-lookup"><span data-stu-id="6ca55-242">FLOAT</span></span> |<span data-ttu-id="6ca55-243">Tek</span><span class="sxs-lookup"><span data-stu-id="6ca55-243">Single</span></span> |
| <span data-ttu-id="6ca55-244">INET</span><span class="sxs-lookup"><span data-stu-id="6ca55-244">INET</span></span> |<span data-ttu-id="6ca55-245">Dize</span><span class="sxs-lookup"><span data-stu-id="6ca55-245">String</span></span> |
| <span data-ttu-id="6ca55-246">INT</span><span class="sxs-lookup"><span data-stu-id="6ca55-246">INT</span></span> |<span data-ttu-id="6ca55-247">Int32</span><span class="sxs-lookup"><span data-stu-id="6ca55-247">Int32</span></span> |
| <span data-ttu-id="6ca55-248">METİN</span><span class="sxs-lookup"><span data-stu-id="6ca55-248">TEXT</span></span> |<span data-ttu-id="6ca55-249">Dize</span><span class="sxs-lookup"><span data-stu-id="6ca55-249">String</span></span> |
| <span data-ttu-id="6ca55-250">ZAMAN DAMGASI</span><span class="sxs-lookup"><span data-stu-id="6ca55-250">TIMESTAMP</span></span> |<span data-ttu-id="6ca55-251">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="6ca55-251">DateTime</span></span> |
| <span data-ttu-id="6ca55-252">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="6ca55-252">TIMEUUID</span></span> |<span data-ttu-id="6ca55-253">GUID</span><span class="sxs-lookup"><span data-stu-id="6ca55-253">Guid</span></span> |
| <span data-ttu-id="6ca55-254">UUID</span><span class="sxs-lookup"><span data-stu-id="6ca55-254">UUID</span></span> |<span data-ttu-id="6ca55-255">GUID</span><span class="sxs-lookup"><span data-stu-id="6ca55-255">Guid</span></span> |
| <span data-ttu-id="6ca55-256">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="6ca55-256">VARCHAR</span></span> |<span data-ttu-id="6ca55-257">Dize</span><span class="sxs-lookup"><span data-stu-id="6ca55-257">String</span></span> |
| <span data-ttu-id="6ca55-258">VARINT</span><span class="sxs-lookup"><span data-stu-id="6ca55-258">VARINT</span></span> |<span data-ttu-id="6ca55-259">Ondalık</span><span class="sxs-lookup"><span data-stu-id="6ca55-259">Decimal</span></span> |

> [!NOTE]
> <span data-ttu-id="6ca55-260">Türleri (harita, kümesi, liste, vb.), başvurmak için koleksiyonu [iş Cassandra koleksiyon türlerini sanal tablosunu kullanarak](#work-with-collections-using-virtual-table) bölümü.</span><span class="sxs-lookup"><span data-stu-id="6ca55-260">For collection types (map, set, list, etc.), refer to [Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.</span></span>
>
> <span data-ttu-id="6ca55-261">Kullanıcı tanımlı türler desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="6ca55-261">User-defined types are not supported.</span></span>
>
> <span data-ttu-id="6ca55-262">İkili sütun ve dize sütunu uzunluklarını uzunluğu 4000'den büyük olamaz.</span><span class="sxs-lookup"><span data-stu-id="6ca55-262">The length of Binary Column and String Column lengths cannot be greater than 4000.</span></span>
>
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="6ca55-263">Sanal tablosunu kullanarak koleksiyonları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="6ca55-263">Work with collections using virtual table</span></span>
<span data-ttu-id="6ca55-264">Azure Data Factory bağlanmak ve Cassandra veritabanınızdan verileri kopyalamak için yerleşik bir ODBC sürücüsü kullanır.</span><span class="sxs-lookup"><span data-stu-id="6ca55-264">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your Cassandra database.</span></span> <span data-ttu-id="6ca55-265">Harita, kümesi ve listesi dahil olmak üzere koleksiyon türü için karşılık gelen sanal tablolara veri sürücüsü renormalizes.</span><span class="sxs-lookup"><span data-stu-id="6ca55-265">For collection types including map, set and list, the driver renormalizes the data into corresponding virtual tables.</span></span> <span data-ttu-id="6ca55-266">Özellikle, bir tablo tüm koleksiyon sütunları içeriyorsa, sürücü aşağıdaki sanal tablolar oluşturur:</span><span class="sxs-lookup"><span data-stu-id="6ca55-266">Specifically, if a table contains any collection columns, the driver generates the following virtual tables:</span></span>

* <span data-ttu-id="6ca55-267">A **temel tablo**, koleksiyon sütunları hariç gerçek tablosu olarak aynı verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="6ca55-267">A **base table**, which contains the same data as the real table except for the collection columns.</span></span> <span data-ttu-id="6ca55-268">Temel tablo aynı adını temsil ettiği gerçek tablo olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="6ca55-268">The base table uses the same name as the real table that it represents.</span></span>
* <span data-ttu-id="6ca55-269">A **sanal tablo** her koleksiyon sütun için hangi genişletir iç içe veri.</span><span class="sxs-lookup"><span data-stu-id="6ca55-269">A **virtual table** for each collection column, which expands the nested data.</span></span> <span data-ttu-id="6ca55-270">Koleksiyonları temsil eden sanal tablolar ayırıcı gerçek tablosunun adı kullanılarak adlandırılmış "*vt*" ve sütunun adı.</span><span class="sxs-lookup"><span data-stu-id="6ca55-270">The virtual tables that represent collections are named using the name of the real table, a separator “*vt*” and the name of the column.</span></span>

<span data-ttu-id="6ca55-271">Sanal tablolar Normalleştirilmemiş verilere erişmek sürücüyü etkinleştirme gerçek tablodaki verileri bakın.</span><span class="sxs-lookup"><span data-stu-id="6ca55-271">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span></span> <span data-ttu-id="6ca55-272">Ayrıntılar için örnek bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="6ca55-272">See Example section for details.</span></span> <span data-ttu-id="6ca55-273">Sorgulamak ve sanal tabloları birleştirme Cassandra koleksiyonların içeriğe erişebilir.</span><span class="sxs-lookup"><span data-stu-id="6ca55-273">You can access the content of Cassandra collections by querying and joining the virtual tables.</span></span>

<span data-ttu-id="6ca55-274">Kullanabileceğiniz [Kopyalama Sihirbazı'nı](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) sezgisel sanal tablolar dahil olmak üzere Cassandra veritabanındaki tabloların listesini görüntülemek ve içindeki verilerin önizlemesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="6ca55-274">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in Cassandra database including the virtual tables, and preview the data inside.</span></span> <span data-ttu-id="6ca55-275">Ayrıca, kopyalama Sihirbazı'nda bir sorgu oluşturun ve sonuçları görmek için Doğrula.</span><span class="sxs-lookup"><span data-stu-id="6ca55-275">You can also construct a query in the Copy Wizard and validate to see the result.</span></span>

### <a name="example"></a><span data-ttu-id="6ca55-276">Örnek</span><span class="sxs-lookup"><span data-stu-id="6ca55-276">Example</span></span>
<span data-ttu-id="6ca55-277">Örneğin, aşağıdaki "ExampleTable", "pk_int", değer adlı bir text sütunu, bir liste sütunu, sütun eşleme ve ("StringSet" olarak adlandırılır) bir sütunu Ayarla adlı bir tamsayı birincil anahtar sütunu içeren bir Cassandra veritabanı tablosu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6ca55-277">For example, the following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span></span>

| <span data-ttu-id="6ca55-278">pk_int</span><span class="sxs-lookup"><span data-stu-id="6ca55-278">pk_int</span></span> | <span data-ttu-id="6ca55-279">Değer</span><span class="sxs-lookup"><span data-stu-id="6ca55-279">Value</span></span> | <span data-ttu-id="6ca55-280">Liste</span><span class="sxs-lookup"><span data-stu-id="6ca55-280">List</span></span> | <span data-ttu-id="6ca55-281">eşleme</span><span class="sxs-lookup"><span data-stu-id="6ca55-281">Map</span></span> | <span data-ttu-id="6ca55-282">StringSet</span><span class="sxs-lookup"><span data-stu-id="6ca55-282">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="6ca55-283">1</span><span class="sxs-lookup"><span data-stu-id="6ca55-283">1</span></span> |<span data-ttu-id="6ca55-284">"örnek değeri 1"</span><span class="sxs-lookup"><span data-stu-id="6ca55-284">"sample value 1"</span></span> |<span data-ttu-id="6ca55-285">["1", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="6ca55-285">["1", "2", "3"]</span></span> |<span data-ttu-id="6ca55-286">{"S1": "a", "S2": "b"}</span><span class="sxs-lookup"><span data-stu-id="6ca55-286">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="6ca55-287">{"A", "B", "C"}</span><span class="sxs-lookup"><span data-stu-id="6ca55-287">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="6ca55-288">3</span><span class="sxs-lookup"><span data-stu-id="6ca55-288">3</span></span> |<span data-ttu-id="6ca55-289">"örnek value 3"</span><span class="sxs-lookup"><span data-stu-id="6ca55-289">"sample value 3"</span></span> |<span data-ttu-id="6ca55-290">["100", "101", "102", "105"]</span><span class="sxs-lookup"><span data-stu-id="6ca55-290">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="6ca55-291">{"S1": "t"}</span><span class="sxs-lookup"><span data-stu-id="6ca55-291">{"S1": "t"}</span></span> |<span data-ttu-id="6ca55-292">{"A", "E"}</span><span class="sxs-lookup"><span data-stu-id="6ca55-292">{"A", "E"}</span></span> |

<span data-ttu-id="6ca55-293">Sürücü bu tek tablo göstermek için birden çok sanal tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6ca55-293">The driver would generate multiple virtual tables to represent this single table.</span></span> <span data-ttu-id="6ca55-294">Sanal tablolardaki yabancı anahtar sütunları gerçek tablosundaki birincil anahtar sütunlarının başvuru ve sanal tablo satırı karşılık gelen gerçek tablo satırı belirtmenize.</span><span class="sxs-lookup"><span data-stu-id="6ca55-294">The foreign key columns in the virtual tables reference the primary key columns in the real table, and indicate which real table row the virtual table row corresponds to.</span></span>

<span data-ttu-id="6ca55-295">İlk sanal "ExampleTable" adlı temel tablo aşağıdaki tabloda gösterilen tablodur.</span><span class="sxs-lookup"><span data-stu-id="6ca55-295">The first virtual table is the base table named “ExampleTable” is shown in the following table.</span></span> <span data-ttu-id="6ca55-296">Temel tablo özgün veritabanı tablosunun bu tablodan atlanmış ve diğer sanal tablolarda genişletilmiş koleksiyonları dışında aynı verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="6ca55-296">The base table contains the same data as the original database table except for the collections, which are omitted from this table and expanded in other virtual tables.</span></span>

| <span data-ttu-id="6ca55-297">pk_int</span><span class="sxs-lookup"><span data-stu-id="6ca55-297">pk_int</span></span> | <span data-ttu-id="6ca55-298">Değer</span><span class="sxs-lookup"><span data-stu-id="6ca55-298">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6ca55-299">1</span><span class="sxs-lookup"><span data-stu-id="6ca55-299">1</span></span> |<span data-ttu-id="6ca55-300">"örnek değeri 1"</span><span class="sxs-lookup"><span data-stu-id="6ca55-300">"sample value 1"</span></span> |
| <span data-ttu-id="6ca55-301">3</span><span class="sxs-lookup"><span data-stu-id="6ca55-301">3</span></span> |<span data-ttu-id="6ca55-302">"örnek value 3"</span><span class="sxs-lookup"><span data-stu-id="6ca55-302">"sample value 3"</span></span> |

<span data-ttu-id="6ca55-303">Aşağıdaki tablolarda listesi, eşleme ve StringSet sütunları verilerden renormalize sanal tablolar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6ca55-303">The following tables show the virtual tables that renormalize the data from the List, Map, and StringSet columns.</span></span> <span data-ttu-id="6ca55-304">Yalnızca "_index" veya "_anahtar" ile biten adlarını sütunlarla özgün listesi veya eşlemesi içinde veri konumunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="6ca55-304">The columns with names that end with “_index” or “_key” indicate the position of the data within the original list or map.</span></span> <span data-ttu-id="6ca55-305">Yalnızca "_value" ile biten adlarını sütunlarla koleksiyondan genişletilmiş verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="6ca55-305">The columns with names that end with “_value” contain the expanded data from the collection.</span></span>

#### <a name="table-exampletablevtlist"></a><span data-ttu-id="6ca55-306">Tablo "ExampleTable_vt_List":</span><span class="sxs-lookup"><span data-stu-id="6ca55-306">Table “ExampleTable_vt_List”:</span></span>
| <span data-ttu-id="6ca55-307">pk_int</span><span class="sxs-lookup"><span data-stu-id="6ca55-307">pk_int</span></span> | <span data-ttu-id="6ca55-308">List_index</span><span class="sxs-lookup"><span data-stu-id="6ca55-308">List_index</span></span> | <span data-ttu-id="6ca55-309">List_value</span><span class="sxs-lookup"><span data-stu-id="6ca55-309">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ca55-310">1</span><span class="sxs-lookup"><span data-stu-id="6ca55-310">1</span></span> |<span data-ttu-id="6ca55-311">0</span><span class="sxs-lookup"><span data-stu-id="6ca55-311">0</span></span> |<span data-ttu-id="6ca55-312">1</span><span class="sxs-lookup"><span data-stu-id="6ca55-312">1</span></span> |
| <span data-ttu-id="6ca55-313">1</span><span class="sxs-lookup"><span data-stu-id="6ca55-313">1</span></span> |<span data-ttu-id="6ca55-314">1</span><span class="sxs-lookup"><span data-stu-id="6ca55-314">1</span></span> |<span data-ttu-id="6ca55-315">2</span><span class="sxs-lookup"><span data-stu-id="6ca55-315">2</span></span> |
| <span data-ttu-id="6ca55-316">1</span><span class="sxs-lookup"><span data-stu-id="6ca55-316">1</span></span> |<span data-ttu-id="6ca55-317">2</span><span class="sxs-lookup"><span data-stu-id="6ca55-317">2</span></span> |<span data-ttu-id="6ca55-318">3</span><span class="sxs-lookup"><span data-stu-id="6ca55-318">3</span></span> |
| <span data-ttu-id="6ca55-319">3</span><span class="sxs-lookup"><span data-stu-id="6ca55-319">3</span></span> |<span data-ttu-id="6ca55-320">0</span><span class="sxs-lookup"><span data-stu-id="6ca55-320">0</span></span> |<span data-ttu-id="6ca55-321">100</span><span class="sxs-lookup"><span data-stu-id="6ca55-321">100</span></span> |
| <span data-ttu-id="6ca55-322">3</span><span class="sxs-lookup"><span data-stu-id="6ca55-322">3</span></span> |<span data-ttu-id="6ca55-323">1</span><span class="sxs-lookup"><span data-stu-id="6ca55-323">1</span></span> |<span data-ttu-id="6ca55-324">101</span><span class="sxs-lookup"><span data-stu-id="6ca55-324">101</span></span> |
| <span data-ttu-id="6ca55-325">3</span><span class="sxs-lookup"><span data-stu-id="6ca55-325">3</span></span> |<span data-ttu-id="6ca55-326">2</span><span class="sxs-lookup"><span data-stu-id="6ca55-326">2</span></span> |<span data-ttu-id="6ca55-327">102</span><span class="sxs-lookup"><span data-stu-id="6ca55-327">102</span></span> |
| <span data-ttu-id="6ca55-328">3</span><span class="sxs-lookup"><span data-stu-id="6ca55-328">3</span></span> |<span data-ttu-id="6ca55-329">3</span><span class="sxs-lookup"><span data-stu-id="6ca55-329">3</span></span> |<span data-ttu-id="6ca55-330">103</span><span class="sxs-lookup"><span data-stu-id="6ca55-330">103</span></span> |

#### <a name="table-exampletablevtmap"></a><span data-ttu-id="6ca55-331">Tablo "ExampleTable_vt_Map":</span><span class="sxs-lookup"><span data-stu-id="6ca55-331">Table “ExampleTable_vt_Map”:</span></span>
| <span data-ttu-id="6ca55-332">pk_int</span><span class="sxs-lookup"><span data-stu-id="6ca55-332">pk_int</span></span> | <span data-ttu-id="6ca55-333">Map_key</span><span class="sxs-lookup"><span data-stu-id="6ca55-333">Map_key</span></span> | <span data-ttu-id="6ca55-334">Map_value</span><span class="sxs-lookup"><span data-stu-id="6ca55-334">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ca55-335">1</span><span class="sxs-lookup"><span data-stu-id="6ca55-335">1</span></span> |<span data-ttu-id="6ca55-336">S1</span><span class="sxs-lookup"><span data-stu-id="6ca55-336">S1</span></span> |<span data-ttu-id="6ca55-337">A</span><span class="sxs-lookup"><span data-stu-id="6ca55-337">A</span></span> |
| <span data-ttu-id="6ca55-338">1</span><span class="sxs-lookup"><span data-stu-id="6ca55-338">1</span></span> |<span data-ttu-id="6ca55-339">S2</span><span class="sxs-lookup"><span data-stu-id="6ca55-339">S2</span></span> |<span data-ttu-id="6ca55-340">B</span><span class="sxs-lookup"><span data-stu-id="6ca55-340">b</span></span> |
| <span data-ttu-id="6ca55-341">3</span><span class="sxs-lookup"><span data-stu-id="6ca55-341">3</span></span> |<span data-ttu-id="6ca55-342">S1</span><span class="sxs-lookup"><span data-stu-id="6ca55-342">S1</span></span> |<span data-ttu-id="6ca55-343">T</span><span class="sxs-lookup"><span data-stu-id="6ca55-343">t</span></span> |

#### <a name="table-exampletablevtstringset"></a><span data-ttu-id="6ca55-344">Tablo "ExampleTable_vt_StringSet":</span><span class="sxs-lookup"><span data-stu-id="6ca55-344">Table “ExampleTable_vt_StringSet”:</span></span>
| <span data-ttu-id="6ca55-345">pk_int</span><span class="sxs-lookup"><span data-stu-id="6ca55-345">pk_int</span></span> | <span data-ttu-id="6ca55-346">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="6ca55-346">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="6ca55-347">1</span><span class="sxs-lookup"><span data-stu-id="6ca55-347">1</span></span> |<span data-ttu-id="6ca55-348">A</span><span class="sxs-lookup"><span data-stu-id="6ca55-348">A</span></span> |
| <span data-ttu-id="6ca55-349">1</span><span class="sxs-lookup"><span data-stu-id="6ca55-349">1</span></span> |<span data-ttu-id="6ca55-350">B</span><span class="sxs-lookup"><span data-stu-id="6ca55-350">B</span></span> |
| <span data-ttu-id="6ca55-351">1</span><span class="sxs-lookup"><span data-stu-id="6ca55-351">1</span></span> |<span data-ttu-id="6ca55-352">C</span><span class="sxs-lookup"><span data-stu-id="6ca55-352">C</span></span> |
| <span data-ttu-id="6ca55-353">3</span><span class="sxs-lookup"><span data-stu-id="6ca55-353">3</span></span> |<span data-ttu-id="6ca55-354">A</span><span class="sxs-lookup"><span data-stu-id="6ca55-354">A</span></span> |
| <span data-ttu-id="6ca55-355">3</span><span class="sxs-lookup"><span data-stu-id="6ca55-355">3</span></span> |<span data-ttu-id="6ca55-356">E</span><span class="sxs-lookup"><span data-stu-id="6ca55-356">E</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="6ca55-357">Kaynak havuzu sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="6ca55-357">Map source to sink columns</span></span>
<span data-ttu-id="6ca55-358">Havuz dataset sütunlara kaynak kümesindeki eşleme sütunları hakkında bilgi edinmek için [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="6ca55-358">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="6ca55-359">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="6ca55-359">Repeatable read from relational sources</span></span>
<span data-ttu-id="6ca55-360">İlişkisel veri kopyalama verileri depoladığında, Yinelenebilirlik istenmeyen sonuçları önlemek için göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="6ca55-360">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="6ca55-361">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ca55-361">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="6ca55-362">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ca55-362">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="6ca55-363">Bir dilim iki yolla yeniden çalıştırıldığında, aynı veri dilimi çalıştırmak kaç kez geçtiğinden bağımsız okuduğunuzdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ca55-363">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="6ca55-364">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="6ca55-364">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="6ca55-365">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="6ca55-365">Performance and Tuning</span></span>
<span data-ttu-id="6ca55-366">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve onu en iyi duruma getirmek için çeşitli yollar etkisi performansını anahtar Etkenler hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="6ca55-366">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
