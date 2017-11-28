---
title: "aaaMove veri öğesinden PostgreSQL Azure Data Factory kullanarak | Microsoft Docs"
description: "Hakkında bilgi edinin Azure Data Factory kullanarak PostgreSQL veritabanından toomove veri."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 888d9ebc-2500-4071-b6d1-0f6bd1b5997c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: ea384f4e06f7d7bedae2949e4ea727c8f8806614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a><span data-ttu-id="73a1d-103">Azure Data Factory kullanarak PostgreSQL taşıma verileri</span><span class="sxs-lookup"><span data-stu-id="73a1d-103">Move data from PostgreSQL using Azure Data Factory</span></span>
<span data-ttu-id="73a1d-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri bir şirket içi PostgreSQL veritabanından açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="73a1d-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises PostgreSQL database.</span></span> <span data-ttu-id="73a1d-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="73a1d-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="73a1d-106">Bir şirket içi PostgreSQL veri deposu desteklenen tooany havuz veri deposundan verileri kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73a1d-106">You can copy data from an on-premises PostgreSQL data store tooany supported sink data store.</span></span> <span data-ttu-id="73a1d-107">Veri depoları havuzlarını hello kopyalama etkinliği tarafından desteklenen bir listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="73a1d-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="73a1d-108">Veri Fabrikası şu anda bir PostgreSQL veri taşınmasını destekler veritabanı tooother veri depoları, ancak verileri diğer veriler taşıma tooan PostgreSQL veritabanına depolar değil için.</span><span class="sxs-lookup"><span data-stu-id="73a1d-108">Data factory currently supports moving data from a PostgreSQL database tooother data stores, but not for moving data from other data stores tooan PostgreSQL database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="73a1d-109">Önkoşulları</span><span class="sxs-lookup"><span data-stu-id="73a1d-109">prerequisites</span></span>

<span data-ttu-id="73a1d-110">Data Factory Hizmeti'ne hello veri yönetimi ağ geçidi kullanarak bağlanan tooon içi PostgreSQL kaynakları destekler.</span><span class="sxs-lookup"><span data-stu-id="73a1d-110">Data Factory service supports connecting tooon-premises PostgreSQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="73a1d-111">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale toolearn veri yönetimi ağ geçidi ve hello ağ geçidi kurun ayarlama hakkında adım adım yönergeleri hakkında.</span><span class="sxs-lookup"><span data-stu-id="73a1d-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="73a1d-112">Bir Azure Iaas sanal Hello PostgreSQL veritabanına barındırılan olsa bile ağ geçidi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="73a1d-112">Gateway is required even if hello PostgreSQL database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="73a1d-113">Ağ geçidi üzerinde aynı Iaas VM hello veri olarak depolamak veya hello ağ geçidi olarak aynı uzunlukta farklı bir VM üzerinde toohello veritabanı bağlanabilir hello yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73a1d-113">You can install gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="73a1d-114">Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="73a1d-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="73a1d-115">Desteklenen sürümleri ve yükleme</span><span class="sxs-lookup"><span data-stu-id="73a1d-115">Supported versions and installation</span></span>
<span data-ttu-id="73a1d-116">Veri Yönetimi ağ geçidi tooconnect toohello PostgreSQL veritabanı için hello yüklemek [PostgreSQL için Ngpsql veri sağlayıcısı](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 veya yukarıdaki üzerinde aynı hello veri yönetimi ağ geçidi hello gibi sistem.</span><span class="sxs-lookup"><span data-stu-id="73a1d-116">For Data Management Gateway tooconnect toohello PostgreSQL Database, install hello [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="73a1d-117">PostgreSQL sürüm 7.4 ve üzeri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="73a1d-117">PostgreSQL version 7.4 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="73a1d-118">Başlarken</span><span class="sxs-lookup"><span data-stu-id="73a1d-118">Getting started</span></span>
<span data-ttu-id="73a1d-119">Farklı araçlar/API'lerini kullanarak bir şirket içi PostgreSQL veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="73a1d-119">You can create a pipeline with a copy activity that moves data from an on-premises PostgreSQL data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="73a1d-120">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="73a1d-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="73a1d-121">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="73a1d-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="73a1d-122">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="73a1d-122">You can also use hello following tools toocreate a pipeline:</span></span> 
    - <span data-ttu-id="73a1d-123">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="73a1d-123">Azure portal</span></span>
    - <span data-ttu-id="73a1d-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="73a1d-124">Visual Studio</span></span>
    - <span data-ttu-id="73a1d-125">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="73a1d-125">Azure PowerShell</span></span>
    - <span data-ttu-id="73a1d-126">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="73a1d-126">Azure Resource Manager template</span></span>
    - <span data-ttu-id="73a1d-127">.NET API’si</span><span class="sxs-lookup"><span data-stu-id="73a1d-127">.NET API</span></span>
    - <span data-ttu-id="73a1d-128">REST API</span><span class="sxs-lookup"><span data-stu-id="73a1d-128">REST API</span></span>

     <span data-ttu-id="73a1d-129">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="73a1d-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="73a1d-130">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="73a1d-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="73a1d-131">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="73a1d-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="73a1d-132">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="73a1d-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="73a1d-133">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="73a1d-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="73a1d-134">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="73a1d-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="73a1d-135">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="73a1d-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="73a1d-136">Bir şirket içi PostgreSQL veri deposundaki kullanılan toocopy verileri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: PostgreSQL tooAzure Blob veri kopyalama](#json-example-copy-data-from-postgresql-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="73a1d-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises PostgreSQL data store, see [JSON example: Copy data from PostgreSQL tooAzure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="73a1d-137">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooa PostgreSQL veri deposu olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="73a1d-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa PostgreSQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="73a1d-138">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="73a1d-138">Linked service properties</span></span>
<span data-ttu-id="73a1d-139">Aşağıdaki tablonun hello JSON öğeleri belirli tooPostgreSQL bağlantılı hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="73a1d-139">hello following table provides description for JSON elements specific tooPostgreSQL linked service.</span></span>

| <span data-ttu-id="73a1d-140">Özellik</span><span class="sxs-lookup"><span data-stu-id="73a1d-140">Property</span></span> | <span data-ttu-id="73a1d-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="73a1d-141">Description</span></span> | <span data-ttu-id="73a1d-142">Gerekli</span><span class="sxs-lookup"><span data-stu-id="73a1d-142">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="73a1d-143">type</span><span class="sxs-lookup"><span data-stu-id="73a1d-143">type</span></span> |<span data-ttu-id="73a1d-144">Merhaba type özelliği ayarlanmalıdır: **OnPremisesPostgreSql**</span><span class="sxs-lookup"><span data-stu-id="73a1d-144">hello type property must be set to: **OnPremisesPostgreSql**</span></span> |<span data-ttu-id="73a1d-145">Evet</span><span class="sxs-lookup"><span data-stu-id="73a1d-145">Yes</span></span> |
| <span data-ttu-id="73a1d-146">sunucu</span><span class="sxs-lookup"><span data-stu-id="73a1d-146">server</span></span> |<span data-ttu-id="73a1d-147">Merhaba PostgreSQL sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="73a1d-147">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="73a1d-148">Evet</span><span class="sxs-lookup"><span data-stu-id="73a1d-148">Yes</span></span> |
| <span data-ttu-id="73a1d-149">Veritabanı</span><span class="sxs-lookup"><span data-stu-id="73a1d-149">database</span></span> |<span data-ttu-id="73a1d-150">Merhaba PostgreSQL veritabanının adı.</span><span class="sxs-lookup"><span data-stu-id="73a1d-150">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="73a1d-151">Evet</span><span class="sxs-lookup"><span data-stu-id="73a1d-151">Yes</span></span> |
| <span data-ttu-id="73a1d-152">Şema</span><span class="sxs-lookup"><span data-stu-id="73a1d-152">schema</span></span> |<span data-ttu-id="73a1d-153">Merhaba veritabanındaki hello şema adı.</span><span class="sxs-lookup"><span data-stu-id="73a1d-153">Name of hello schema in hello database.</span></span> <span data-ttu-id="73a1d-154">Merhaba şema adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="73a1d-154">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="73a1d-155">Hayır</span><span class="sxs-lookup"><span data-stu-id="73a1d-155">No</span></span> |
| <span data-ttu-id="73a1d-156">authenticationType</span><span class="sxs-lookup"><span data-stu-id="73a1d-156">authenticationType</span></span> |<span data-ttu-id="73a1d-157">Kimlik doğrulama türü tooconnect toohello PostgreSQL veritabanına kullanılır.</span><span class="sxs-lookup"><span data-stu-id="73a1d-157">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="73a1d-158">Olası değerler şunlardır: Anonim, temel ve Windows.</span><span class="sxs-lookup"><span data-stu-id="73a1d-158">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="73a1d-159">Evet</span><span class="sxs-lookup"><span data-stu-id="73a1d-159">Yes</span></span> |
| <span data-ttu-id="73a1d-160">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="73a1d-160">username</span></span> |<span data-ttu-id="73a1d-161">Temel veya Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="73a1d-161">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="73a1d-162">Hayır</span><span class="sxs-lookup"><span data-stu-id="73a1d-162">No</span></span> |
| <span data-ttu-id="73a1d-163">password</span><span class="sxs-lookup"><span data-stu-id="73a1d-163">password</span></span> |<span data-ttu-id="73a1d-164">Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="73a1d-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="73a1d-165">Hayır</span><span class="sxs-lookup"><span data-stu-id="73a1d-165">No</span></span> |
| <span data-ttu-id="73a1d-166">gatewayName</span><span class="sxs-lookup"><span data-stu-id="73a1d-166">gatewayName</span></span> |<span data-ttu-id="73a1d-167">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi PostgreSQL veritabanına kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="73a1d-167">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="73a1d-168">Evet</span><span class="sxs-lookup"><span data-stu-id="73a1d-168">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="73a1d-169">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="73a1d-169">Dataset properties</span></span>
<span data-ttu-id="73a1d-170">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="73a1d-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="73a1d-171">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri kümesi türleri için benzerdir.</span><span class="sxs-lookup"><span data-stu-id="73a1d-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="73a1d-172">Merhaba typeProperties bölümü veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="73a1d-172">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="73a1d-173">Merhaba typeProperties bölüm türü veri kümesi için **RelationalTable** (PostgreSQL veri kümesi içeren) hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="73a1d-173">hello typeProperties section for dataset of type **RelationalTable** (which includes PostgreSQL dataset) has hello following properties:</span></span>

| <span data-ttu-id="73a1d-174">Özellik</span><span class="sxs-lookup"><span data-stu-id="73a1d-174">Property</span></span> | <span data-ttu-id="73a1d-175">Açıklama</span><span class="sxs-lookup"><span data-stu-id="73a1d-175">Description</span></span> | <span data-ttu-id="73a1d-176">Gerekli</span><span class="sxs-lookup"><span data-stu-id="73a1d-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="73a1d-177">tableName</span><span class="sxs-lookup"><span data-stu-id="73a1d-177">tableName</span></span> |<span data-ttu-id="73a1d-178">Merhaba bağlı PostgreSQL veritabanı örneğinde Merhaba tablonun adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="73a1d-178">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="73a1d-179">Merhaba tableName büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="73a1d-179">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="73a1d-180">Hayır (varsa **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="73a1d-180">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="73a1d-181">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="73a1d-181">Copy activity properties</span></span>
<span data-ttu-id="73a1d-182">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="73a1d-182">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="73a1d-183">Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="73a1d-183">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="73a1d-184">Oysa hello typeProperties bölümünde hello etkinlik özellikleri her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="73a1d-184">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="73a1d-185">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="73a1d-185">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="73a1d-186">Kaynak türü olduğunda **RelationalSource** (içeren PostgreSQL), aşağıdaki özelliklere hello typeProperties bölümünde bulunur:</span><span class="sxs-lookup"><span data-stu-id="73a1d-186">When source is of type **RelationalSource** (which includes PostgreSQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="73a1d-187">Özellik</span><span class="sxs-lookup"><span data-stu-id="73a1d-187">Property</span></span> | <span data-ttu-id="73a1d-188">Açıklama</span><span class="sxs-lookup"><span data-stu-id="73a1d-188">Description</span></span> | <span data-ttu-id="73a1d-189">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="73a1d-189">Allowed values</span></span> | <span data-ttu-id="73a1d-190">Gerekli</span><span class="sxs-lookup"><span data-stu-id="73a1d-190">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="73a1d-191">sorgu</span><span class="sxs-lookup"><span data-stu-id="73a1d-191">query</span></span> |<span data-ttu-id="73a1d-192">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="73a1d-192">Use hello custom query tooread data.</span></span> |<span data-ttu-id="73a1d-193">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="73a1d-193">SQL query string.</span></span> <span data-ttu-id="73a1d-194">Örneğin: "sorgu": "seçin * gelen \"MySchema\".\" MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="73a1d-194">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="73a1d-195">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="73a1d-195">No (if **tableName** of **dataset** is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="73a1d-196">Şema ve tablo adları büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="73a1d-196">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="73a1d-197">Bunları içine `""` (çift tırnak) hello sorgu.</span><span class="sxs-lookup"><span data-stu-id="73a1d-197">Enclose them in `""` (double quotes) in hello query.</span></span>  

<span data-ttu-id="73a1d-198">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="73a1d-198">**Example:**</span></span>

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-tooazure-blob"></a><span data-ttu-id="73a1d-199">JSON örnek: PostgreSQL tooAzure Blob veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="73a1d-199">JSON example: Copy data from PostgreSQL tooAzure Blob</span></span>
<span data-ttu-id="73a1d-200">Bu örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="73a1d-200">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="73a1d-201">Bunların nasıl tooAzure Blob Storage PostgreSQL toocopy verilerden veritabanı gösterir.</span><span class="sxs-lookup"><span data-stu-id="73a1d-201">They show how toocopy data from PostgreSQL database tooAzure Blob Storage.</span></span> <span data-ttu-id="73a1d-202">Ancak, veri belirtildiği hello havuzlarını, kopyalanan tooany olabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="73a1d-202">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="73a1d-203">Bu örnek, JSON parçacıklarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="73a1d-203">This sample provides JSON snippets.</span></span> <span data-ttu-id="73a1d-204">Merhaba veri fabrikası oluşturma için yönergeler içermez.</span><span class="sxs-lookup"><span data-stu-id="73a1d-204">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="73a1d-205">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="73a1d-205">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="73a1d-206">Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="73a1d-206">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="73a1d-207">Bağlı hizmet türü [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="73a1d-207">A linked service of type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="73a1d-208">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="73a1d-208">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="73a1d-209">Bir giriş [dataset](data-factory-create-datasets.md) türü [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="73a1d-209">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="73a1d-210">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="73a1d-210">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="73a1d-211">Merhaba [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="73a1d-211">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="73a1d-212">Merhaba örnek veri PostgreSQL veritabanına tooa blob bir sorgu sonucunda her saat kopyalar.</span><span class="sxs-lookup"><span data-stu-id="73a1d-212">hello sample copies data from a query result in PostgreSQL database tooa blob every hour.</span></span> <span data-ttu-id="73a1d-213">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="73a1d-213">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="73a1d-214">İlk adım olarak, hello veri yönetimi ağ geçidi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="73a1d-214">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="73a1d-215">Merhaba yönergelerdir hello [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="73a1d-215">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="73a1d-216">**Bağlantılı PostgreSQL hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="73a1d-216">**PostgreSQL linked service:**</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
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
<span data-ttu-id="73a1d-217">**Azure Blob storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="73a1d-217">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
    }
    }
}
```
<span data-ttu-id="73a1d-218">**PostgreSQL girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="73a1d-218">**PostgreSQL input dataset:**</span></span>

<span data-ttu-id="73a1d-219">Merhaba örnek bir tablo "MyTable" PostgreSQL içinde oluşturduğunuz ve zaman serisi veri için "zaman damgası" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="73a1d-219">hello sample assumes you have created a table “MyTable” in PostgreSQL and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="73a1d-220">Ayarı `"external": true` hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil bildirir.</span><span class="sxs-lookup"><span data-stu-id="73a1d-220">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
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

<span data-ttu-id="73a1d-221">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="73a1d-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="73a1d-222">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="73a1d-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="73a1d-223">Merhaba klasör yolu ve dosya adını hello blob dinamik olarak değerlendirilir işleniyor hello dilimin hello başlangıç zamanı temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="73a1d-223">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="73a1d-224">Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="73a1d-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobPostgreSqlDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/postgresql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="73a1d-225">**Kopyalama etkinliği ile kanal:**</span><span class="sxs-lookup"><span data-stu-id="73a1d-225">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="73a1d-226">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun saatlik ise.</span><span class="sxs-lookup"><span data-stu-id="73a1d-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="73a1d-227">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**RelationalSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="73a1d-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="73a1d-228">Merhaba belirtilen hello SQL sorgusu **sorgu** özelliği hello PostgreSQL veritabanında hello public.usstates tablosundan hello veri seçer.</span><span class="sxs-lookup"><span data-stu-id="73a1d-228">hello SQL query specified for hello **query** property selects hello data from hello public.usstates table in hello PostgreSQL database.</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"public\".\"usstates\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "PostgreSqlDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobPostgreSqlDataSet"
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
                "name": "PostgreSqlToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
## <a name="type-mapping-for-postgresql"></a><span data-ttu-id="73a1d-229">Tür eşlemesi için PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="73a1d-229">Type mapping for PostgreSQL</span></span>
<span data-ttu-id="73a1d-230">Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale kopyalama etkinliği ile 2 adımlı yaklaşımı izleyerek hello kaynak türleri toosink türlerinden otomatik tür dönüşümleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="73a1d-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="73a1d-231">Yerel kaynak türleri too.NET türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="73a1d-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="73a1d-232">.NET türü toonative havuz türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="73a1d-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="73a1d-233">Veri tooPostgreSQL taşırken hello aşağıdaki eşlemelerini PostgreSQL türü too.NET türünden kullanılır.</span><span class="sxs-lookup"><span data-stu-id="73a1d-233">When moving data tooPostgreSQL, hello following mappings are used from PostgreSQL type too.NET type.</span></span>

| <span data-ttu-id="73a1d-234">Bir PostgreSQL veritabanı türü</span><span class="sxs-lookup"><span data-stu-id="73a1d-234">PostgreSQL Database type</span></span> | <span data-ttu-id="73a1d-235">PostgresSQL diğer adlar</span><span class="sxs-lookup"><span data-stu-id="73a1d-235">PostgresSQL aliases</span></span> | <span data-ttu-id="73a1d-236">.NET framework türü</span><span class="sxs-lookup"><span data-stu-id="73a1d-236">.NET Framework type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="73a1d-237">abstime</span><span class="sxs-lookup"><span data-stu-id="73a1d-237">abstime</span></span> | |<span data-ttu-id="73a1d-238">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="73a1d-238">Datetime</span></span> | &nbsp;
| <span data-ttu-id="73a1d-239">bigint</span><span class="sxs-lookup"><span data-stu-id="73a1d-239">bigint</span></span> |<span data-ttu-id="73a1d-240">int8</span><span class="sxs-lookup"><span data-stu-id="73a1d-240">int8</span></span> |<span data-ttu-id="73a1d-241">Int64</span><span class="sxs-lookup"><span data-stu-id="73a1d-241">Int64</span></span> |
| <span data-ttu-id="73a1d-242">bigserial</span><span class="sxs-lookup"><span data-stu-id="73a1d-242">bigserial</span></span> |<span data-ttu-id="73a1d-243">serial8</span><span class="sxs-lookup"><span data-stu-id="73a1d-243">serial8</span></span> |<span data-ttu-id="73a1d-244">Int64</span><span class="sxs-lookup"><span data-stu-id="73a1d-244">Int64</span></span> |
| <span data-ttu-id="73a1d-245">bit [(n)]</span><span class="sxs-lookup"><span data-stu-id="73a1d-245">bit [ (n) ]</span></span> | |<span data-ttu-id="73a1d-246">Byte [], dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-246">Byte[], String</span></span> | &nbsp;
| <span data-ttu-id="73a1d-247">değişen [(n)] bit</span><span class="sxs-lookup"><span data-stu-id="73a1d-247">bit varying [ (n) ]</span></span> |<span data-ttu-id="73a1d-248">varbit</span><span class="sxs-lookup"><span data-stu-id="73a1d-248">varbit</span></span> |<span data-ttu-id="73a1d-249">Byte [], dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-249">Byte[], String</span></span> |
| <span data-ttu-id="73a1d-250">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="73a1d-250">boolean</span></span> |<span data-ttu-id="73a1d-251">bool</span><span class="sxs-lookup"><span data-stu-id="73a1d-251">bool</span></span> |<span data-ttu-id="73a1d-252">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="73a1d-252">Boolean</span></span> |
| <span data-ttu-id="73a1d-253">Kutusu</span><span class="sxs-lookup"><span data-stu-id="73a1d-253">box</span></span> | |<span data-ttu-id="73a1d-254">Byte [], dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-254">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="73a1d-255">bytea</span><span class="sxs-lookup"><span data-stu-id="73a1d-255">bytea</span></span> | |<span data-ttu-id="73a1d-256">Byte [], dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-256">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="73a1d-257">karakter [(n)]</span><span class="sxs-lookup"><span data-stu-id="73a1d-257">character [ (n) ]</span></span> |<span data-ttu-id="73a1d-258">char [(n)]</span><span class="sxs-lookup"><span data-stu-id="73a1d-258">char [ (n) ]</span></span> |<span data-ttu-id="73a1d-259">Dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-259">String</span></span> |
| <span data-ttu-id="73a1d-260">[(n)] değişen karakter</span><span class="sxs-lookup"><span data-stu-id="73a1d-260">character varying [ (n) ]</span></span> |<span data-ttu-id="73a1d-261">varchar [(n)]</span><span class="sxs-lookup"><span data-stu-id="73a1d-261">varchar [ (n) ]</span></span> |<span data-ttu-id="73a1d-262">Dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-262">String</span></span> |
| <span data-ttu-id="73a1d-263">CID</span><span class="sxs-lookup"><span data-stu-id="73a1d-263">cid</span></span> | |<span data-ttu-id="73a1d-264">Dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-264">String</span></span> |&nbsp;
| <span data-ttu-id="73a1d-265">CIDR</span><span class="sxs-lookup"><span data-stu-id="73a1d-265">cidr</span></span> | |<span data-ttu-id="73a1d-266">Dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-266">String</span></span> |&nbsp;
| <span data-ttu-id="73a1d-267">Daire</span><span class="sxs-lookup"><span data-stu-id="73a1d-267">circle</span></span> | |<span data-ttu-id="73a1d-268">Byte [], dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-268">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="73a1d-269">Tarih</span><span class="sxs-lookup"><span data-stu-id="73a1d-269">date</span></span> | |<span data-ttu-id="73a1d-270">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="73a1d-270">Datetime</span></span> |&nbsp;
| <span data-ttu-id="73a1d-271">daterange</span><span class="sxs-lookup"><span data-stu-id="73a1d-271">daterange</span></span> | |<span data-ttu-id="73a1d-272">Dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-272">String</span></span> |&nbsp;
| <span data-ttu-id="73a1d-273">çift duyarlıklı</span><span class="sxs-lookup"><span data-stu-id="73a1d-273">double precision</span></span> |<span data-ttu-id="73a1d-274">FLOAT8</span><span class="sxs-lookup"><span data-stu-id="73a1d-274">float8</span></span> |<span data-ttu-id="73a1d-275">Çift</span><span class="sxs-lookup"><span data-stu-id="73a1d-275">Double</span></span> |
| <span data-ttu-id="73a1d-276">INet</span><span class="sxs-lookup"><span data-stu-id="73a1d-276">inet</span></span> | |<span data-ttu-id="73a1d-277">Byte [], dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-277">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="73a1d-278">intarry</span><span class="sxs-lookup"><span data-stu-id="73a1d-278">intarry</span></span> | |<span data-ttu-id="73a1d-279">Dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-279">String</span></span> |&nbsp;
| <span data-ttu-id="73a1d-280">int4range</span><span class="sxs-lookup"><span data-stu-id="73a1d-280">int4range</span></span> | |<span data-ttu-id="73a1d-281">Dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-281">String</span></span> |&nbsp;
| <span data-ttu-id="73a1d-282">int8range</span><span class="sxs-lookup"><span data-stu-id="73a1d-282">int8range</span></span> | |<span data-ttu-id="73a1d-283">Dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-283">String</span></span> |&nbsp;
| <span data-ttu-id="73a1d-284">tamsayı</span><span class="sxs-lookup"><span data-stu-id="73a1d-284">integer</span></span> |<span data-ttu-id="73a1d-285">int, int4</span><span class="sxs-lookup"><span data-stu-id="73a1d-285">int, int4</span></span> |<span data-ttu-id="73a1d-286">Int32</span><span class="sxs-lookup"><span data-stu-id="73a1d-286">Int32</span></span> |
| <span data-ttu-id="73a1d-287">aralığı [alanlar] [(p)]</span><span class="sxs-lookup"><span data-stu-id="73a1d-287">interval [ fields ] [ (p) ]</span></span> | |<span data-ttu-id="73a1d-288">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="73a1d-288">Timespan</span></span> |&nbsp;
| <span data-ttu-id="73a1d-289">JSON</span><span class="sxs-lookup"><span data-stu-id="73a1d-289">json</span></span> | |<span data-ttu-id="73a1d-290">Dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-290">String</span></span> |&nbsp;
| <span data-ttu-id="73a1d-291">jsonb</span><span class="sxs-lookup"><span data-stu-id="73a1d-291">jsonb</span></span> | |<span data-ttu-id="73a1d-292">Byte]</span><span class="sxs-lookup"><span data-stu-id="73a1d-292">Byte[]</span></span> |&nbsp;
| <span data-ttu-id="73a1d-293">Satır</span><span class="sxs-lookup"><span data-stu-id="73a1d-293">line</span></span> | |<span data-ttu-id="73a1d-294">Byte [], dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-294">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="73a1d-295">lseg</span><span class="sxs-lookup"><span data-stu-id="73a1d-295">lseg</span></span> | |<span data-ttu-id="73a1d-296">Byte [], dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-296">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="73a1d-297">macaddr</span><span class="sxs-lookup"><span data-stu-id="73a1d-297">macaddr</span></span> | |<span data-ttu-id="73a1d-298">Byte [], dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-298">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="73a1d-299">para</span><span class="sxs-lookup"><span data-stu-id="73a1d-299">money</span></span> | |<span data-ttu-id="73a1d-300">Ondalık</span><span class="sxs-lookup"><span data-stu-id="73a1d-300">Decimal</span></span> |&nbsp;
| <span data-ttu-id="73a1d-301">sayısal [(p, s)]</span><span class="sxs-lookup"><span data-stu-id="73a1d-301">numeric [ (p, s) ]</span></span> |<span data-ttu-id="73a1d-302">ondalık [(p, s)]</span><span class="sxs-lookup"><span data-stu-id="73a1d-302">decimal [ (p, s) ]</span></span> |<span data-ttu-id="73a1d-303">Ondalık</span><span class="sxs-lookup"><span data-stu-id="73a1d-303">Decimal</span></span> |
| <span data-ttu-id="73a1d-304">numrange</span><span class="sxs-lookup"><span data-stu-id="73a1d-304">numrange</span></span> | |<span data-ttu-id="73a1d-305">Dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-305">String</span></span> |&nbsp;
| <span data-ttu-id="73a1d-306">OID</span><span class="sxs-lookup"><span data-stu-id="73a1d-306">oid</span></span> | |<span data-ttu-id="73a1d-307">Int32</span><span class="sxs-lookup"><span data-stu-id="73a1d-307">Int32</span></span> |&nbsp;
| <span data-ttu-id="73a1d-308">Yol</span><span class="sxs-lookup"><span data-stu-id="73a1d-308">path</span></span> | |<span data-ttu-id="73a1d-309">Byte [], dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-309">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="73a1d-310">pg_lsn</span><span class="sxs-lookup"><span data-stu-id="73a1d-310">pg_lsn</span></span> | |<span data-ttu-id="73a1d-311">Int64</span><span class="sxs-lookup"><span data-stu-id="73a1d-311">Int64</span></span> |&nbsp;
| <span data-ttu-id="73a1d-312">noktası</span><span class="sxs-lookup"><span data-stu-id="73a1d-312">point</span></span> | |<span data-ttu-id="73a1d-313">Byte [], dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-313">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="73a1d-314">Çokgen</span><span class="sxs-lookup"><span data-stu-id="73a1d-314">polygon</span></span> | |<span data-ttu-id="73a1d-315">Byte [], dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-315">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="73a1d-316">Gerçek</span><span class="sxs-lookup"><span data-stu-id="73a1d-316">real</span></span> |<span data-ttu-id="73a1d-317">float4</span><span class="sxs-lookup"><span data-stu-id="73a1d-317">float4</span></span> |<span data-ttu-id="73a1d-318">Tek</span><span class="sxs-lookup"><span data-stu-id="73a1d-318">Single</span></span> |
| <span data-ttu-id="73a1d-319">tamsayı</span><span class="sxs-lookup"><span data-stu-id="73a1d-319">smallint</span></span> |<span data-ttu-id="73a1d-320">int2</span><span class="sxs-lookup"><span data-stu-id="73a1d-320">int2</span></span> |<span data-ttu-id="73a1d-321">Int16</span><span class="sxs-lookup"><span data-stu-id="73a1d-321">Int16</span></span> |
| <span data-ttu-id="73a1d-322">smallserial</span><span class="sxs-lookup"><span data-stu-id="73a1d-322">smallserial</span></span> |<span data-ttu-id="73a1d-323">serial2</span><span class="sxs-lookup"><span data-stu-id="73a1d-323">serial2</span></span> |<span data-ttu-id="73a1d-324">Int16</span><span class="sxs-lookup"><span data-stu-id="73a1d-324">Int16</span></span> |
| <span data-ttu-id="73a1d-325">Seri</span><span class="sxs-lookup"><span data-stu-id="73a1d-325">serial</span></span> |<span data-ttu-id="73a1d-326">serial4</span><span class="sxs-lookup"><span data-stu-id="73a1d-326">serial4</span></span> |<span data-ttu-id="73a1d-327">Int32</span><span class="sxs-lookup"><span data-stu-id="73a1d-327">Int32</span></span> |
| <span data-ttu-id="73a1d-328">Metin</span><span class="sxs-lookup"><span data-stu-id="73a1d-328">text</span></span> | |<span data-ttu-id="73a1d-329">Dize</span><span class="sxs-lookup"><span data-stu-id="73a1d-329">String</span></span> |&nbsp;

## <a name="map-source-toosink-columns"></a><span data-ttu-id="73a1d-330">Kaynak toosink sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="73a1d-330">Map source toosink columns</span></span>
<span data-ttu-id="73a1d-331">Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="73a1d-331">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="73a1d-332">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="73a1d-332">Repeatable read from relational sources</span></span>
<span data-ttu-id="73a1d-333">İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları.</span><span class="sxs-lookup"><span data-stu-id="73a1d-333">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="73a1d-334">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73a1d-334">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="73a1d-335">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73a1d-335">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="73a1d-336">Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="73a1d-336">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="73a1d-337">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="73a1d-337">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="73a1d-338">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="73a1d-338">Performance and Tuning</span></span>
<span data-ttu-id="73a1d-339">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="73a1d-339">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
