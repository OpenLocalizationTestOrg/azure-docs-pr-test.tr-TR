---
title: Data Factory kullanarak Cassandra aaaMove verilerden | Microsoft Docs
description: "Azure Data Factory kullanarak bir şirket içi Cassandra toomove verileri nasıl veritabanı hakkında bilgi edinin."
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
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a><span data-ttu-id="228c8-103">Azure Data Factory kullanarak bir şirket içi Cassandra veritabanından veri taşıma</span><span class="sxs-lookup"><span data-stu-id="228c8-103">Move data from an on-premises Cassandra database using Azure Data Factory</span></span>
<span data-ttu-id="228c8-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri bir şirket içi Cassandra veritabanından açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="228c8-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Cassandra database.</span></span> <span data-ttu-id="228c8-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="228c8-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="228c8-106">Bir şirket içi Cassandra veri deposu desteklenen tooany havuz veri deposundan verileri kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="228c8-106">You can copy data from an on-premises Cassandra data store tooany supported sink data store.</span></span> <span data-ttu-id="228c8-107">Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="228c8-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="228c8-108">Veri Fabrikası şu anda verileri Cassandra verilerinden tooother veri depolarına depolamak taşıma yalnızca, ancak diğer veri depoları tooa Cassandra veri deposundan veri taşıma değil destekler.</span><span class="sxs-lookup"><span data-stu-id="228c8-108">Data factory currently supports only moving data from a Cassandra data store tooother data stores, but not for moving data from other data stores tooa Cassandra data store.</span></span> 

## <a name="supported-versions"></a><span data-ttu-id="228c8-109">Desteklenen sürümler</span><span class="sxs-lookup"><span data-stu-id="228c8-109">Supported versions</span></span>
<span data-ttu-id="228c8-110">Merhaba Cassandra bağlayıcı Cassandra sürümleri aşağıdaki hello destekler: 2.X.</span><span class="sxs-lookup"><span data-stu-id="228c8-110">hello Cassandra connector supports hello following versions of Cassandra: 2.X.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="228c8-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="228c8-111">Prerequisites</span></span>
<span data-ttu-id="228c8-112">Hello Azure Data Factory hizmeti toobe mümkün tooconnect tooyour şirket içi Cassandra veritabanı için veri yönetimi ağ geçidi yüklemeniz gerekir hello üzerinde aynı ana bilgisayar hello veritabanının makine veya hello kaynaklarla için rekabet ayrı makine tooavoid Veritabanı.</span><span class="sxs-lookup"><span data-stu-id="228c8-112">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises Cassandra database, you must install a Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="228c8-113">Veri Yönetimi ağ geçidi, şirket içi veri kaynakları toocloud Hizmetleri güvenli ve yönetilen bir şekilde birbirine bağlayan bir bileşenidir.</span><span class="sxs-lookup"><span data-stu-id="228c8-113">Data Management Gateway is a component that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="228c8-114">Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) makale veri yönetimi ağ geçidi hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="228c8-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="228c8-115">Bkz: [şirket içi toocloud veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale hello ağ geçidi veri ardışık düzen toomove veri ayarlama hakkında adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="228c8-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="228c8-116">Merhaba veritabanı hello bulutta, örneğin, bir Azure Iaas sanal bile barındırılıyorsa hello ağ geçidi tooconnect tooa Cassandra veritabanı kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="228c8-116">You must use hello gateway tooconnect tooa Cassandra database even if hello database is hosted in hello cloud, for example, on an Azure IaaS VM.</span></span> <span data-ttu-id="228c8-117">Y hello ağ geçidine sahip ana hello veritabanının aynı VM hello veya hello ağ geçidi olarak uzunluğunda ayrı bir VM'de toohello veritabanı bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="228c8-117">Y You can have hello gateway on hello same VM that hosts hello database or on a separate VM as long as hello gateway can connect toohello database.</span></span>  

<span data-ttu-id="228c8-118">Merhaba ağ geçidi yüklediğinizde, bir Microsoft Cassandra ODBC sürücüsü kullanılan tooconnect tooCassandra veritabanı otomatik olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="228c8-118">When you install hello gateway, it automatically installs a Microsoft Cassandra ODBC driver used tooconnect tooCassandra database.</span></span> <span data-ttu-id="228c8-119">Bu nedenle, gerekmeyen toomanually hello Cassandra veritabanından veri kopyalama işlemi sırasında bu herhangi bir sürücüsü hello ağ geçidi makineye yükleyin.</span><span class="sxs-lookup"><span data-stu-id="228c8-119">Therefore, you don't need toomanually install any driver on hello gateway machine when copying data from hello Cassandra database.</span></span> 

> [!NOTE]
> <span data-ttu-id="228c8-120">Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="228c8-120">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="228c8-121">Başlarken</span><span class="sxs-lookup"><span data-stu-id="228c8-121">Getting started</span></span>
<span data-ttu-id="228c8-122">Farklı araçlar/API'lerini kullanarak bir şirket içi Cassandra veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="228c8-122">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="228c8-123">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="228c8-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="228c8-124">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="228c8-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="228c8-125">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="228c8-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="228c8-126">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="228c8-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="228c8-127">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="228c8-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="228c8-128">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="228c8-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="228c8-129">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="228c8-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="228c8-130">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="228c8-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="228c8-131">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="228c8-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="228c8-132">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="228c8-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="228c8-133">Bir şirket içi Cassandra veri deposundaki kullanılan toocopy verileri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: Cassandra tooAzure Blob veri kopyalama](#json-example-copy-data-from-cassandra-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="228c8-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra tooAzure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="228c8-134">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooa Cassandra veri deposu olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="228c8-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Cassandra data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="228c8-135">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="228c8-135">Linked service properties</span></span>
<span data-ttu-id="228c8-136">Aşağıdaki tablonun hello JSON öğeleri belirli tooCassandra bağlantılı hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="228c8-136">hello following table provides description for JSON elements specific tooCassandra linked service.</span></span>

| <span data-ttu-id="228c8-137">Özellik</span><span class="sxs-lookup"><span data-stu-id="228c8-137">Property</span></span> | <span data-ttu-id="228c8-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="228c8-138">Description</span></span> | <span data-ttu-id="228c8-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="228c8-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="228c8-140">type</span><span class="sxs-lookup"><span data-stu-id="228c8-140">type</span></span> |<span data-ttu-id="228c8-141">Merhaba type özelliği ayarlanmalıdır: **OnPremisesCassandra**</span><span class="sxs-lookup"><span data-stu-id="228c8-141">hello type property must be set to: **OnPremisesCassandra**</span></span> |<span data-ttu-id="228c8-142">Evet</span><span class="sxs-lookup"><span data-stu-id="228c8-142">Yes</span></span> |
| <span data-ttu-id="228c8-143">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="228c8-143">host</span></span> |<span data-ttu-id="228c8-144">Bir veya daha fazla IP adresleri veya ana bilgisayar adlarını Cassandra sunucuları.</span><span class="sxs-lookup"><span data-stu-id="228c8-144">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="228c8-145">IP adresi veya ana bilgisayar adları tooconnect tooall sunucuları virgülle ayrılmış listesini eşzamanlı olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="228c8-145">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="228c8-146">Evet</span><span class="sxs-lookup"><span data-stu-id="228c8-146">Yes</span></span> |
| <span data-ttu-id="228c8-147">port</span><span class="sxs-lookup"><span data-stu-id="228c8-147">port</span></span> |<span data-ttu-id="228c8-148">Merhaba Cassandra sunucu hello TCP bağlantı noktası toolisten istemci bağlantıları için kullanır.</span><span class="sxs-lookup"><span data-stu-id="228c8-148">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="228c8-149">Hayır, varsayılan değer: 9042</span><span class="sxs-lookup"><span data-stu-id="228c8-149">No, default value: 9042</span></span> |
| <span data-ttu-id="228c8-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="228c8-150">authenticationType</span></span> |<span data-ttu-id="228c8-151">Basic veya Anonymous</span><span class="sxs-lookup"><span data-stu-id="228c8-151">Basic, or Anonymous</span></span> |<span data-ttu-id="228c8-152">Evet</span><span class="sxs-lookup"><span data-stu-id="228c8-152">Yes</span></span> |
| <span data-ttu-id="228c8-153">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="228c8-153">username</span></span> |<span data-ttu-id="228c8-154">Merhaba kullanıcı hesabının kullanıcı adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="228c8-154">Specify user name for hello user account.</span></span> |<span data-ttu-id="228c8-155">Evet, authenticationType tooBasic ayarlarsanız.</span><span class="sxs-lookup"><span data-stu-id="228c8-155">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="228c8-156">password</span><span class="sxs-lookup"><span data-stu-id="228c8-156">password</span></span> |<span data-ttu-id="228c8-157">Merhaba kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="228c8-157">Specify password for hello user account.</span></span> |<span data-ttu-id="228c8-158">Evet, authenticationType tooBasic ayarlarsanız.</span><span class="sxs-lookup"><span data-stu-id="228c8-158">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="228c8-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="228c8-159">gatewayName</span></span> |<span data-ttu-id="228c8-160">kullanılan tooconnect toohello şirket içi Cassandra veritabanı hello ağ geçidi Hello adı.</span><span class="sxs-lookup"><span data-stu-id="228c8-160">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="228c8-161">Evet</span><span class="sxs-lookup"><span data-stu-id="228c8-161">Yes</span></span> |
| <span data-ttu-id="228c8-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="228c8-162">encryptedCredential</span></span> |<span data-ttu-id="228c8-163">Merhaba ağ geçidi tarafından şifrelenmiş kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="228c8-163">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="228c8-164">Hayır</span><span class="sxs-lookup"><span data-stu-id="228c8-164">No</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="228c8-165">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="228c8-165">Dataset properties</span></span>
<span data-ttu-id="228c8-166">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="228c8-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="228c8-167">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="228c8-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="228c8-168">Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="228c8-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="228c8-169">Merhaba typeProperties bölüm türü veri kümesi için **CassandraTable** hello aşağıdaki özelliklere sahip</span><span class="sxs-lookup"><span data-stu-id="228c8-169">hello typeProperties section for dataset of type **CassandraTable** has hello following properties</span></span>

| <span data-ttu-id="228c8-170">Özellik</span><span class="sxs-lookup"><span data-stu-id="228c8-170">Property</span></span> | <span data-ttu-id="228c8-171">Açıklama</span><span class="sxs-lookup"><span data-stu-id="228c8-171">Description</span></span> | <span data-ttu-id="228c8-172">Gerekli</span><span class="sxs-lookup"><span data-stu-id="228c8-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="228c8-173">keyspace</span><span class="sxs-lookup"><span data-stu-id="228c8-173">keyspace</span></span> |<span data-ttu-id="228c8-174">Merhaba keyspace veya Cassandra veritabanındaki şema adı.</span><span class="sxs-lookup"><span data-stu-id="228c8-174">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="228c8-175">Evet (varsa **sorgu** için **CassandraSource** tanımlı değil).</span><span class="sxs-lookup"><span data-stu-id="228c8-175">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="228c8-176">tableName</span><span class="sxs-lookup"><span data-stu-id="228c8-176">tableName</span></span> |<span data-ttu-id="228c8-177">Cassandra veritabanındaki Merhaba tablonun adı.</span><span class="sxs-lookup"><span data-stu-id="228c8-177">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="228c8-178">Evet (varsa **sorgu** için **CassandraSource** tanımlı değil).</span><span class="sxs-lookup"><span data-stu-id="228c8-178">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="228c8-179">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="228c8-179">Copy activity properties</span></span>
<span data-ttu-id="228c8-180">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="228c8-180">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="228c8-181">Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="228c8-181">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="228c8-182">Oysa hello typeProperties bölümünde hello etkinlik özellikleri her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="228c8-182">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="228c8-183">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="228c8-183">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="228c8-184">Kaynak türü olduğunda **CassandraSource**, aşağıdaki özelliklere hello typeProperties bölümünde bulunur:</span><span class="sxs-lookup"><span data-stu-id="228c8-184">When source is of type **CassandraSource**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="228c8-185">Özellik</span><span class="sxs-lookup"><span data-stu-id="228c8-185">Property</span></span> | <span data-ttu-id="228c8-186">Açıklama</span><span class="sxs-lookup"><span data-stu-id="228c8-186">Description</span></span> | <span data-ttu-id="228c8-187">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="228c8-187">Allowed values</span></span> | <span data-ttu-id="228c8-188">Gerekli</span><span class="sxs-lookup"><span data-stu-id="228c8-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="228c8-189">sorgu</span><span class="sxs-lookup"><span data-stu-id="228c8-189">query</span></span> |<span data-ttu-id="228c8-190">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="228c8-190">Use hello custom query tooread data.</span></span> |<span data-ttu-id="228c8-191">SQL-92 sorgusu veya CQL sorgusu.</span><span class="sxs-lookup"><span data-stu-id="228c8-191">SQL-92 query or CQL query.</span></span> <span data-ttu-id="228c8-192">Bkz: [CQL başvuru](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="228c8-192">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="228c8-193">SQL sorgusu kullanırken belirtin **keyspace name.table adı** tooquery istediğiniz toorepresent hello tablo.</span><span class="sxs-lookup"><span data-stu-id="228c8-193">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="228c8-194">Hayır (tableName ve veri kümesi üzerinde keyspace tanımlanmışsa).</span><span class="sxs-lookup"><span data-stu-id="228c8-194">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="228c8-195">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="228c8-195">consistencyLevel</span></span> |<span data-ttu-id="228c8-196">kaç tane çoğaltmaları veri toohello istemci uygulaması döndürmeden önce tooa Okuma isteği yanıtlamalısınız Hello tutarlılık düzeyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="228c8-196">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="228c8-197">İstek veri toosatisfy hello okumak için Cassandra denetimleri çoğaltmaları belirtilen sayıda hello.</span><span class="sxs-lookup"><span data-stu-id="228c8-197">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="228c8-198">BİR, İKİ, ÜÇ, ÇEKİRDEK, TÜMÜ, LOCAL_QUORUM EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="228c8-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="228c8-199">Bkz: [veri tutarlılığını yapılandırma](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="228c8-199">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="228c8-200">Hayır.</span><span class="sxs-lookup"><span data-stu-id="228c8-200">No.</span></span> <span data-ttu-id="228c8-201">Varsayılan değer biridir.</span><span class="sxs-lookup"><span data-stu-id="228c8-201">Default value is ONE.</span></span> |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a><span data-ttu-id="228c8-202">JSON örnek: Cassandra tooAzure Blob veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="228c8-202">JSON example: Copy data from Cassandra tooAzure Blob</span></span>
<span data-ttu-id="228c8-203">Bu örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="228c8-203">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="228c8-204">Bu, nasıl bir şirket içi Cassandra toocopy verileri Azure Blob Storage tooan veritabanı gösterir.</span><span class="sxs-lookup"><span data-stu-id="228c8-204">It shows how toocopy data from an on-premises Cassandra database tooan Azure Blob Storage.</span></span> <span data-ttu-id="228c8-205">Ancak, veri belirtildiği hello havuzlarını, kopyalanan tooany olabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="228c8-205">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="228c8-206">Bu örnek, JSON parçacıklarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="228c8-206">This sample provides JSON snippets.</span></span> <span data-ttu-id="228c8-207">Merhaba veri fabrikası oluşturma için yönergeler içermez.</span><span class="sxs-lookup"><span data-stu-id="228c8-207">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="228c8-208">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="228c8-208">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="228c8-209">Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="228c8-209">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="228c8-210">Bağlı hizmet türü [OnPremisesCassandra](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="228c8-210">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span></span>
* <span data-ttu-id="228c8-211">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="228c8-211">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="228c8-212">Bir giriş [dataset](data-factory-create-datasets.md) türü [CassandraTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="228c8-212">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span></span>
* <span data-ttu-id="228c8-213">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="228c8-213">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="228c8-214">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [CassandraSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="228c8-214">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="228c8-215">**Bağlantılı Cassandra hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="228c8-215">**Cassandra linked service:**</span></span>

<span data-ttu-id="228c8-216">Bu örnek hello kullanır **Cassandra** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="228c8-216">This example uses hello **Cassandra** linked service.</span></span> <span data-ttu-id="228c8-217">Bkz: [Cassandra bağlantılı hizmeti](#linked-service-properties) bu bağlantılı hizmet tarafından desteklenen hello özellikler bölümü.</span><span class="sxs-lookup"><span data-stu-id="228c8-217">See [Cassandra linked service](#linked-service-properties) section for hello properties supported by this linked service.</span></span>  

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

<span data-ttu-id="228c8-218">**Azure Storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="228c8-218">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="228c8-219">**Cassandra girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="228c8-219">**Cassandra input dataset:**</span></span>

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

<span data-ttu-id="228c8-220">Ayarı **dış** çok**true** hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil bildirir.</span><span class="sxs-lookup"><span data-stu-id="228c8-220">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="228c8-221">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="228c8-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="228c8-222">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="228c8-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

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

<span data-ttu-id="228c8-223">**Etkinlik Cassandra kaynak ve Blob havuz sahip işlem hattı kopyalayın:**</span><span class="sxs-lookup"><span data-stu-id="228c8-223">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span></span>

<span data-ttu-id="228c8-224">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="228c8-224">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="228c8-225">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**CassandraSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="228c8-225">In hello pipeline JSON definition, hello **source** type is set too**CassandraSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="228c8-226">Bkz: [RelationalSource türü özellikleri](#copy-activity-properties) hello RelationalSource hello tarafından desteklenen özelliklerin listesi için.</span><span class="sxs-lookup"><span data-stu-id="228c8-226">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties supported by hello RelationalSource.</span></span>

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
            "description": "Copy from Cassandra tooan Azure blob",
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

### <a name="type-mapping-for-cassandra"></a><span data-ttu-id="228c8-227">Tür eşlemesi için Cassandra</span><span class="sxs-lookup"><span data-stu-id="228c8-227">Type mapping for Cassandra</span></span>
| <span data-ttu-id="228c8-228">Cassandra türü</span><span class="sxs-lookup"><span data-stu-id="228c8-228">Cassandra Type</span></span> | <span data-ttu-id="228c8-229">.NET türü temelinde</span><span class="sxs-lookup"><span data-stu-id="228c8-229">.Net Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="228c8-230">ASCII</span><span class="sxs-lookup"><span data-stu-id="228c8-230">ASCII</span></span> |<span data-ttu-id="228c8-231">Dize</span><span class="sxs-lookup"><span data-stu-id="228c8-231">String</span></span> |
| <span data-ttu-id="228c8-232">BIGINT</span><span class="sxs-lookup"><span data-stu-id="228c8-232">BIGINT</span></span> |<span data-ttu-id="228c8-233">Int64</span><span class="sxs-lookup"><span data-stu-id="228c8-233">Int64</span></span> |
| <span data-ttu-id="228c8-234">BLOB</span><span class="sxs-lookup"><span data-stu-id="228c8-234">BLOB</span></span> |<span data-ttu-id="228c8-235">Byte]</span><span class="sxs-lookup"><span data-stu-id="228c8-235">Byte[]</span></span> |
| <span data-ttu-id="228c8-236">BOOLE DEĞERİ</span><span class="sxs-lookup"><span data-stu-id="228c8-236">BOOLEAN</span></span> |<span data-ttu-id="228c8-237">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="228c8-237">Boolean</span></span> |
| <span data-ttu-id="228c8-238">ONDALIK</span><span class="sxs-lookup"><span data-stu-id="228c8-238">DECIMAL</span></span> |<span data-ttu-id="228c8-239">Ondalık</span><span class="sxs-lookup"><span data-stu-id="228c8-239">Decimal</span></span> |
| <span data-ttu-id="228c8-240">ÇİFT</span><span class="sxs-lookup"><span data-stu-id="228c8-240">DOUBLE</span></span> |<span data-ttu-id="228c8-241">Çift</span><span class="sxs-lookup"><span data-stu-id="228c8-241">Double</span></span> |
| <span data-ttu-id="228c8-242">KAYAN NOKTA</span><span class="sxs-lookup"><span data-stu-id="228c8-242">FLOAT</span></span> |<span data-ttu-id="228c8-243">Tek</span><span class="sxs-lookup"><span data-stu-id="228c8-243">Single</span></span> |
| <span data-ttu-id="228c8-244">INET</span><span class="sxs-lookup"><span data-stu-id="228c8-244">INET</span></span> |<span data-ttu-id="228c8-245">Dize</span><span class="sxs-lookup"><span data-stu-id="228c8-245">String</span></span> |
| <span data-ttu-id="228c8-246">INT</span><span class="sxs-lookup"><span data-stu-id="228c8-246">INT</span></span> |<span data-ttu-id="228c8-247">Int32</span><span class="sxs-lookup"><span data-stu-id="228c8-247">Int32</span></span> |
| <span data-ttu-id="228c8-248">METİN</span><span class="sxs-lookup"><span data-stu-id="228c8-248">TEXT</span></span> |<span data-ttu-id="228c8-249">Dize</span><span class="sxs-lookup"><span data-stu-id="228c8-249">String</span></span> |
| <span data-ttu-id="228c8-250">ZAMAN DAMGASI</span><span class="sxs-lookup"><span data-stu-id="228c8-250">TIMESTAMP</span></span> |<span data-ttu-id="228c8-251">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="228c8-251">DateTime</span></span> |
| <span data-ttu-id="228c8-252">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="228c8-252">TIMEUUID</span></span> |<span data-ttu-id="228c8-253">GUID</span><span class="sxs-lookup"><span data-stu-id="228c8-253">Guid</span></span> |
| <span data-ttu-id="228c8-254">UUID</span><span class="sxs-lookup"><span data-stu-id="228c8-254">UUID</span></span> |<span data-ttu-id="228c8-255">GUID</span><span class="sxs-lookup"><span data-stu-id="228c8-255">Guid</span></span> |
| <span data-ttu-id="228c8-256">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="228c8-256">VARCHAR</span></span> |<span data-ttu-id="228c8-257">Dize</span><span class="sxs-lookup"><span data-stu-id="228c8-257">String</span></span> |
| <span data-ttu-id="228c8-258">VARINT</span><span class="sxs-lookup"><span data-stu-id="228c8-258">VARINT</span></span> |<span data-ttu-id="228c8-259">Ondalık</span><span class="sxs-lookup"><span data-stu-id="228c8-259">Decimal</span></span> |

> [!NOTE]
> <span data-ttu-id="228c8-260">Koleksiyon için türlerini (harita, kümesi, liste, vb.), çok başvurun[iş Cassandra koleksiyon türlerini sanal tablosunu kullanarak](#work-with-collections-using-virtual-table) bölümü.</span><span class="sxs-lookup"><span data-stu-id="228c8-260">For collection types (map, set, list, etc.), refer too[Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.</span></span>
>
> <span data-ttu-id="228c8-261">Kullanıcı tanımlı türler desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="228c8-261">User-defined types are not supported.</span></span>
>
> <span data-ttu-id="228c8-262">İkili sütun ve dize sütunu uzunluklarını Hello uzunluğu 4000'den büyük olamaz.</span><span class="sxs-lookup"><span data-stu-id="228c8-262">hello length of Binary Column and String Column lengths cannot be greater than 4000.</span></span>
>
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="228c8-263">Sanal tablosunu kullanarak koleksiyonları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="228c8-263">Work with collections using virtual table</span></span>
<span data-ttu-id="228c8-264">Azure Data Factory yerleşik ODBC sürücüsü tooconnect tooand kopya veri Cassandra veritabanınızdan kullanır.</span><span class="sxs-lookup"><span data-stu-id="228c8-264">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your Cassandra database.</span></span> <span data-ttu-id="228c8-265">Harita, kümesi ve listesi dahil olmak üzere koleksiyon türü için karşılık gelen sanal tablolara hello veri hello sürücü renormalizes.</span><span class="sxs-lookup"><span data-stu-id="228c8-265">For collection types including map, set and list, hello driver renormalizes hello data into corresponding virtual tables.</span></span> <span data-ttu-id="228c8-266">Bir tablo tüm koleksiyon sütunları içeriyorsa, özellikle hello sürücü sanal tablolar aşağıdaki hello oluşturur:</span><span class="sxs-lookup"><span data-stu-id="228c8-266">Specifically, if a table contains any collection columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="228c8-267">A **temel tablo**, içeren hello hello gerçek tablo hello koleksiyonu sütunları dışında aynı verileri.</span><span class="sxs-lookup"><span data-stu-id="228c8-267">A **base table**, which contains hello same data as hello real table except for hello collection columns.</span></span> <span data-ttu-id="228c8-268">Merhaba temel tablo aynı adı hello temsil ettiği hello gerçek tablo olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="228c8-268">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="228c8-269">A **sanal tablo** her koleksiyon sütun için hangi genişletir hello iç içe geçmiş verileri.</span><span class="sxs-lookup"><span data-stu-id="228c8-269">A **virtual table** for each collection column, which expands hello nested data.</span></span> <span data-ttu-id="228c8-270">koleksiyonları temsil eden hello sanal tablolar Merhaba tablonun adı hello gerçek, ayırıcı kullanılarak adlandırılması "*vt*" ve hello sütunun hello adı.</span><span class="sxs-lookup"><span data-stu-id="228c8-270">hello virtual tables that represent collections are named using hello name of hello real table, a separator “*vt*” and hello name of hello column.</span></span>

<span data-ttu-id="228c8-271">Sanal tablolar hello gerçek tablosunda toohello veri bakın, etkinleştirme hello sürücü tooaccess Normalleştirilmemiş veri hello.</span><span class="sxs-lookup"><span data-stu-id="228c8-271">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="228c8-272">Ayrıntılar için örnek bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="228c8-272">See Example section for details.</span></span> <span data-ttu-id="228c8-273">Sorgulamak ve hello sanal tabloları birleştirme Cassandra koleksiyonların hello içeriğe erişebilir.</span><span class="sxs-lookup"><span data-stu-id="228c8-273">You can access hello content of Cassandra collections by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="228c8-274">Merhaba kullanabilirsiniz [Kopyalama Sihirbazı'nı](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively görünümü hello hello sanal tablolar dahil olmak üzere Cassandra veritabanındaki tabloların listesi ve önizleme içindeki hello verileri.</span><span class="sxs-lookup"><span data-stu-id="228c8-274">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in Cassandra database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="228c8-275">Ayrıca, hello Kopyalama Sihirbazı, bir sorgu oluşturun ve toosee hello sonucu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="228c8-275">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="228c8-276">Örnek</span><span class="sxs-lookup"><span data-stu-id="228c8-276">Example</span></span>
<span data-ttu-id="228c8-277">Örneğin, hello aşağıdaki "ExampleTable" "pk_int", değer adlı bir text sütunu, bir liste sütunu, sütun eşleme ve ("StringSet" olarak adlandırılır) bir sütunu Ayarla adlı bir tamsayı birincil anahtar sütunu içeren bir Cassandra veritabanı tablosu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="228c8-277">For example, hello following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span></span>

| <span data-ttu-id="228c8-278">pk_int</span><span class="sxs-lookup"><span data-stu-id="228c8-278">pk_int</span></span> | <span data-ttu-id="228c8-279">Değer</span><span class="sxs-lookup"><span data-stu-id="228c8-279">Value</span></span> | <span data-ttu-id="228c8-280">Liste</span><span class="sxs-lookup"><span data-stu-id="228c8-280">List</span></span> | <span data-ttu-id="228c8-281">eşleme</span><span class="sxs-lookup"><span data-stu-id="228c8-281">Map</span></span> | <span data-ttu-id="228c8-282">StringSet</span><span class="sxs-lookup"><span data-stu-id="228c8-282">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="228c8-283">1</span><span class="sxs-lookup"><span data-stu-id="228c8-283">1</span></span> |<span data-ttu-id="228c8-284">"örnek değeri 1"</span><span class="sxs-lookup"><span data-stu-id="228c8-284">"sample value 1"</span></span> |<span data-ttu-id="228c8-285">["1", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="228c8-285">["1", "2", "3"]</span></span> |<span data-ttu-id="228c8-286">{"S1": "a", "S2": "b"}</span><span class="sxs-lookup"><span data-stu-id="228c8-286">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="228c8-287">{"A", "B", "C"}</span><span class="sxs-lookup"><span data-stu-id="228c8-287">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="228c8-288">3</span><span class="sxs-lookup"><span data-stu-id="228c8-288">3</span></span> |<span data-ttu-id="228c8-289">"örnek value 3"</span><span class="sxs-lookup"><span data-stu-id="228c8-289">"sample value 3"</span></span> |<span data-ttu-id="228c8-290">["100", "101", "102", "105"]</span><span class="sxs-lookup"><span data-stu-id="228c8-290">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="228c8-291">{"S1": "t"}</span><span class="sxs-lookup"><span data-stu-id="228c8-291">{"S1": "t"}</span></span> |<span data-ttu-id="228c8-292">{"A", "E"}</span><span class="sxs-lookup"><span data-stu-id="228c8-292">{"A", "E"}</span></span> |

<span data-ttu-id="228c8-293">Merhaba sürücüsü birden çok sanal tablolar toorepresent bu tek tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="228c8-293">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="228c8-294">Merhaba hello Sanal tablolardaki yabancı anahtar sütunları hello gerçek tablosundaki birincil anahtar sütunlarının hello başvuru ve hangi gerçek belirtmek tablo hello sanal tablosuna satır karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="228c8-294">hello foreign key columns in hello virtual tables reference hello primary key columns in hello real table, and indicate which real table row hello virtual table row corresponds to.</span></span>

<span data-ttu-id="228c8-295">Aşağıdaki tablonun hello "ExampleTable" adlı hello temel tabloda gösterilen Hello ilk sanal tablosu değil.</span><span class="sxs-lookup"><span data-stu-id="228c8-295">hello first virtual table is hello base table named “ExampleTable” is shown in hello following table.</span></span> <span data-ttu-id="228c8-296">Merhaba temel tablo içeren hello hello özgün veritabanı tablosu bu tablodan atlanmış ve diğer sanal tablolarda genişletilmiş hello koleksiyonları dışında aynı verileri.</span><span class="sxs-lookup"><span data-stu-id="228c8-296">hello base table contains hello same data as hello original database table except for hello collections, which are omitted from this table and expanded in other virtual tables.</span></span>

| <span data-ttu-id="228c8-297">pk_int</span><span class="sxs-lookup"><span data-stu-id="228c8-297">pk_int</span></span> | <span data-ttu-id="228c8-298">Değer</span><span class="sxs-lookup"><span data-stu-id="228c8-298">Value</span></span> |
| --- | --- |
| <span data-ttu-id="228c8-299">1</span><span class="sxs-lookup"><span data-stu-id="228c8-299">1</span></span> |<span data-ttu-id="228c8-300">"örnek değeri 1"</span><span class="sxs-lookup"><span data-stu-id="228c8-300">"sample value 1"</span></span> |
| <span data-ttu-id="228c8-301">3</span><span class="sxs-lookup"><span data-stu-id="228c8-301">3</span></span> |<span data-ttu-id="228c8-302">"örnek value 3"</span><span class="sxs-lookup"><span data-stu-id="228c8-302">"sample value 3"</span></span> |

<span data-ttu-id="228c8-303">Merhaba aşağıdaki tablolarda hello listesi, eşleme ve StringSet sütunları hello verilerden renormalize hello sanal tablolar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="228c8-303">hello following tables show hello virtual tables that renormalize hello data from hello List, Map, and StringSet columns.</span></span> <span data-ttu-id="228c8-304">yalnızca "_index" veya "_anahtar" ile biten adlarını Hello sütunlarla hello asıl liste veya eşlemesi içinde hello veri hello konumunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="228c8-304">hello columns with names that end with “_index” or “_key” indicate hello position of hello data within hello original list or map.</span></span> <span data-ttu-id="228c8-305">yalnızca "_value" ile biten adlarını Hello sütunlarla hello koleksiyonundan hello genişletilmiş verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="228c8-305">hello columns with names that end with “_value” contain hello expanded data from hello collection.</span></span>

#### <a name="table-exampletablevtlist"></a><span data-ttu-id="228c8-306">Tablo "ExampleTable_vt_List":</span><span class="sxs-lookup"><span data-stu-id="228c8-306">Table “ExampleTable_vt_List”:</span></span>
| <span data-ttu-id="228c8-307">pk_int</span><span class="sxs-lookup"><span data-stu-id="228c8-307">pk_int</span></span> | <span data-ttu-id="228c8-308">List_index</span><span class="sxs-lookup"><span data-stu-id="228c8-308">List_index</span></span> | <span data-ttu-id="228c8-309">List_value</span><span class="sxs-lookup"><span data-stu-id="228c8-309">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="228c8-310">1</span><span class="sxs-lookup"><span data-stu-id="228c8-310">1</span></span> |<span data-ttu-id="228c8-311">0</span><span class="sxs-lookup"><span data-stu-id="228c8-311">0</span></span> |<span data-ttu-id="228c8-312">1</span><span class="sxs-lookup"><span data-stu-id="228c8-312">1</span></span> |
| <span data-ttu-id="228c8-313">1</span><span class="sxs-lookup"><span data-stu-id="228c8-313">1</span></span> |<span data-ttu-id="228c8-314">1</span><span class="sxs-lookup"><span data-stu-id="228c8-314">1</span></span> |<span data-ttu-id="228c8-315">2</span><span class="sxs-lookup"><span data-stu-id="228c8-315">2</span></span> |
| <span data-ttu-id="228c8-316">1</span><span class="sxs-lookup"><span data-stu-id="228c8-316">1</span></span> |<span data-ttu-id="228c8-317">2</span><span class="sxs-lookup"><span data-stu-id="228c8-317">2</span></span> |<span data-ttu-id="228c8-318">3</span><span class="sxs-lookup"><span data-stu-id="228c8-318">3</span></span> |
| <span data-ttu-id="228c8-319">3</span><span class="sxs-lookup"><span data-stu-id="228c8-319">3</span></span> |<span data-ttu-id="228c8-320">0</span><span class="sxs-lookup"><span data-stu-id="228c8-320">0</span></span> |<span data-ttu-id="228c8-321">100</span><span class="sxs-lookup"><span data-stu-id="228c8-321">100</span></span> |
| <span data-ttu-id="228c8-322">3</span><span class="sxs-lookup"><span data-stu-id="228c8-322">3</span></span> |<span data-ttu-id="228c8-323">1</span><span class="sxs-lookup"><span data-stu-id="228c8-323">1</span></span> |<span data-ttu-id="228c8-324">101</span><span class="sxs-lookup"><span data-stu-id="228c8-324">101</span></span> |
| <span data-ttu-id="228c8-325">3</span><span class="sxs-lookup"><span data-stu-id="228c8-325">3</span></span> |<span data-ttu-id="228c8-326">2</span><span class="sxs-lookup"><span data-stu-id="228c8-326">2</span></span> |<span data-ttu-id="228c8-327">102</span><span class="sxs-lookup"><span data-stu-id="228c8-327">102</span></span> |
| <span data-ttu-id="228c8-328">3</span><span class="sxs-lookup"><span data-stu-id="228c8-328">3</span></span> |<span data-ttu-id="228c8-329">3</span><span class="sxs-lookup"><span data-stu-id="228c8-329">3</span></span> |<span data-ttu-id="228c8-330">103</span><span class="sxs-lookup"><span data-stu-id="228c8-330">103</span></span> |

#### <a name="table-exampletablevtmap"></a><span data-ttu-id="228c8-331">Tablo "ExampleTable_vt_Map":</span><span class="sxs-lookup"><span data-stu-id="228c8-331">Table “ExampleTable_vt_Map”:</span></span>
| <span data-ttu-id="228c8-332">pk_int</span><span class="sxs-lookup"><span data-stu-id="228c8-332">pk_int</span></span> | <span data-ttu-id="228c8-333">Map_key</span><span class="sxs-lookup"><span data-stu-id="228c8-333">Map_key</span></span> | <span data-ttu-id="228c8-334">Map_value</span><span class="sxs-lookup"><span data-stu-id="228c8-334">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="228c8-335">1</span><span class="sxs-lookup"><span data-stu-id="228c8-335">1</span></span> |<span data-ttu-id="228c8-336">S1</span><span class="sxs-lookup"><span data-stu-id="228c8-336">S1</span></span> |<span data-ttu-id="228c8-337">A</span><span class="sxs-lookup"><span data-stu-id="228c8-337">A</span></span> |
| <span data-ttu-id="228c8-338">1</span><span class="sxs-lookup"><span data-stu-id="228c8-338">1</span></span> |<span data-ttu-id="228c8-339">S2</span><span class="sxs-lookup"><span data-stu-id="228c8-339">S2</span></span> |<span data-ttu-id="228c8-340">B</span><span class="sxs-lookup"><span data-stu-id="228c8-340">b</span></span> |
| <span data-ttu-id="228c8-341">3</span><span class="sxs-lookup"><span data-stu-id="228c8-341">3</span></span> |<span data-ttu-id="228c8-342">S1</span><span class="sxs-lookup"><span data-stu-id="228c8-342">S1</span></span> |<span data-ttu-id="228c8-343">T</span><span class="sxs-lookup"><span data-stu-id="228c8-343">t</span></span> |

#### <a name="table-exampletablevtstringset"></a><span data-ttu-id="228c8-344">Tablo "ExampleTable_vt_StringSet":</span><span class="sxs-lookup"><span data-stu-id="228c8-344">Table “ExampleTable_vt_StringSet”:</span></span>
| <span data-ttu-id="228c8-345">pk_int</span><span class="sxs-lookup"><span data-stu-id="228c8-345">pk_int</span></span> | <span data-ttu-id="228c8-346">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="228c8-346">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="228c8-347">1</span><span class="sxs-lookup"><span data-stu-id="228c8-347">1</span></span> |<span data-ttu-id="228c8-348">A</span><span class="sxs-lookup"><span data-stu-id="228c8-348">A</span></span> |
| <span data-ttu-id="228c8-349">1</span><span class="sxs-lookup"><span data-stu-id="228c8-349">1</span></span> |<span data-ttu-id="228c8-350">B</span><span class="sxs-lookup"><span data-stu-id="228c8-350">B</span></span> |
| <span data-ttu-id="228c8-351">1</span><span class="sxs-lookup"><span data-stu-id="228c8-351">1</span></span> |<span data-ttu-id="228c8-352">C</span><span class="sxs-lookup"><span data-stu-id="228c8-352">C</span></span> |
| <span data-ttu-id="228c8-353">3</span><span class="sxs-lookup"><span data-stu-id="228c8-353">3</span></span> |<span data-ttu-id="228c8-354">A</span><span class="sxs-lookup"><span data-stu-id="228c8-354">A</span></span> |
| <span data-ttu-id="228c8-355">3</span><span class="sxs-lookup"><span data-stu-id="228c8-355">3</span></span> |<span data-ttu-id="228c8-356">E</span><span class="sxs-lookup"><span data-stu-id="228c8-356">E</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="228c8-357">Kaynak toosink sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="228c8-357">Map source toosink columns</span></span>
<span data-ttu-id="228c8-358">Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="228c8-358">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="228c8-359">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="228c8-359">Repeatable read from relational sources</span></span>
<span data-ttu-id="228c8-360">İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları.</span><span class="sxs-lookup"><span data-stu-id="228c8-360">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="228c8-361">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="228c8-361">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="228c8-362">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="228c8-362">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="228c8-363">Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="228c8-363">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="228c8-364">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="228c8-364">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="228c8-365">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="228c8-365">Performance and Tuning</span></span>
<span data-ttu-id="228c8-366">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="228c8-366">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
