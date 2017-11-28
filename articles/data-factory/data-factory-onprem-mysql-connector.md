---
title: Azure Data Factory kullanarak MySQL aaaMove verilerden | Microsoft Docs
description: "Azure Data Factory kullanarak MySQL toomove verileri nasıl veritabanı hakkında bilgi edinin."
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
ms.openlocfilehash: 3ffe969e42ce1a54b265c4739df43fdc594ea891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="6bb6d-103">Veri öğesinden MySQL Azure Data Factory kullanarak Taşı</span><span class="sxs-lookup"><span data-stu-id="6bb6d-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="6bb6d-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri bir şirket içi MySQL veritabanından açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MySQL database.</span></span> <span data-ttu-id="6bb6d-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="6bb6d-106">Bir şirket içi MySQL veri deposu desteklenen tooany havuz veri deposundan verileri kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-106">You can copy data from an on-premises MySQL data store tooany supported sink data store.</span></span> <span data-ttu-id="6bb6d-107">Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="6bb6d-108">Veri Fabrikası şu anda verileri MySQL verilerinden tooother veri depolarına depolamak taşıma yalnızca, ancak diğer veri depoları tooan MySQL veri deposundan veri taşıma değil destekler.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-108">Data factory currently supports only moving data from a MySQL data store tooother data stores, but not for moving data from other data stores tooan MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6bb6d-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6bb6d-109">Prerequisites</span></span>
<span data-ttu-id="6bb6d-110">Data Factory Hizmeti'ne hello veri yönetimi ağ geçidi kullanarak bağlanan tooon içi MySQL kaynakları destekler.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-110">Data Factory service supports connecting tooon-premises MySQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="6bb6d-111">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale toolearn veri yönetimi ağ geçidi ve hello ağ geçidi kurun ayarlama hakkında adım adım yönergeleri hakkında.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="6bb6d-112">Merhaba MySQL veritabanı bir Azure Iaas sanal makine (VM) barındırılan olsa bile ağ geçidi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-112">Gateway is required even if hello MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="6bb6d-113">Merhaba ağ geçidi üzerinde aynı VM hello veri olarak depolamak veya hello ağ geçidi olarak aynı uzunlukta farklı bir VM üzerinde toohello veritabanı bağlanabilir hello yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-113">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="6bb6d-114">Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="6bb6d-115">Desteklenen sürümleri ve yükleme</span><span class="sxs-lookup"><span data-stu-id="6bb6d-115">Supported versions and installation</span></span>
<span data-ttu-id="6bb6d-116">Veri Yönetimi ağ geçidi tooconnect toohello için MySQL veritabanı, ihtiyacınız tooinstall hello [MySQL Connector/Net için Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (sürüm 6.6.5 veya üstü) üzerinde hello aynı veri yönetimi ağ geçidi hello gibi sistem.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-116">For Data Management Gateway tooconnect toohello MySQL Database, you need tooinstall hello [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 or above) on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="6bb6d-117">MySQL sürüm 5.1 ve üzeri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-117">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> <span data-ttu-id="6bb6d-118">Hata İsabet durumunda "Merhaba uzak taraf hello aktarım akışı. kapatıldığı için kimlik doğrulaması başarısız", tooupgrade hello MySQL Connector/Net toohigher sürüm göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-118">If you hit error on "Authentication failed because hello remote party has closed hello transport stream.", consider tooupgrade hello MySQL Connector/Net toohigher version.</span></span>

## <a name="getting-started"></a><span data-ttu-id="6bb6d-119">Başlarken</span><span class="sxs-lookup"><span data-stu-id="6bb6d-119">Getting started</span></span>
<span data-ttu-id="6bb6d-120">Farklı araçlar/API'lerini kullanarak bir şirket içi Cassandra veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-120">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="6bb6d-121">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="6bb6d-122">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="6bb6d-123">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6bb6d-124">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="6bb6d-125">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="6bb6d-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="6bb6d-126">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="6bb6d-127">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="6bb6d-128">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="6bb6d-129">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="6bb6d-130">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="6bb6d-131">Bir şirket içi MySQL veri deposundaki kullanılan toocopy verileri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: MySQL tooAzure Blob veri kopyalama](#json-example-copy-data-from-mysql-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="6bb6d-132">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooa MySQL veri deposu olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="6bb6d-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="6bb6d-133">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="6bb6d-133">Linked service properties</span></span>
<span data-ttu-id="6bb6d-134">Aşağıdaki tablonun hello JSON öğeleri belirli tooMySQL bağlantılı hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-134">hello following table provides description for JSON elements specific tooMySQL linked service.</span></span>

| <span data-ttu-id="6bb6d-135">Özellik</span><span class="sxs-lookup"><span data-stu-id="6bb6d-135">Property</span></span> | <span data-ttu-id="6bb6d-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6bb6d-136">Description</span></span> | <span data-ttu-id="6bb6d-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6bb6d-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6bb6d-138">type</span><span class="sxs-lookup"><span data-stu-id="6bb6d-138">type</span></span> |<span data-ttu-id="6bb6d-139">Merhaba type özelliği ayarlanmalıdır: **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="6bb6d-139">hello type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="6bb6d-140">Evet</span><span class="sxs-lookup"><span data-stu-id="6bb6d-140">Yes</span></span> |
| <span data-ttu-id="6bb6d-141">sunucu</span><span class="sxs-lookup"><span data-stu-id="6bb6d-141">server</span></span> |<span data-ttu-id="6bb6d-142">Merhaba MySQL sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-142">Name of hello MySQL server.</span></span> |<span data-ttu-id="6bb6d-143">Evet</span><span class="sxs-lookup"><span data-stu-id="6bb6d-143">Yes</span></span> |
| <span data-ttu-id="6bb6d-144">Veritabanı</span><span class="sxs-lookup"><span data-stu-id="6bb6d-144">database</span></span> |<span data-ttu-id="6bb6d-145">Merhaba MySQL veritabanının adı.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-145">Name of hello MySQL database.</span></span> |<span data-ttu-id="6bb6d-146">Evet</span><span class="sxs-lookup"><span data-stu-id="6bb6d-146">Yes</span></span> |
| <span data-ttu-id="6bb6d-147">Şema</span><span class="sxs-lookup"><span data-stu-id="6bb6d-147">schema</span></span> |<span data-ttu-id="6bb6d-148">Merhaba veritabanındaki hello şema adı.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-148">Name of hello schema in hello database.</span></span> |<span data-ttu-id="6bb6d-149">Hayır</span><span class="sxs-lookup"><span data-stu-id="6bb6d-149">No</span></span> |
| <span data-ttu-id="6bb6d-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="6bb6d-150">authenticationType</span></span> |<span data-ttu-id="6bb6d-151">Kimlik doğrulama türü tooconnect toohello MySQL veritabanı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-151">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="6bb6d-152">Olası değerler şunlardır: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-152">Possible values are: `Basic`.</span></span> |<span data-ttu-id="6bb6d-153">Evet</span><span class="sxs-lookup"><span data-stu-id="6bb6d-153">Yes</span></span> |
| <span data-ttu-id="6bb6d-154">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="6bb6d-154">username</span></span> |<span data-ttu-id="6bb6d-155">Kullanıcı adı tooconnect toohello MySQL veritabanı belirtin.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-155">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="6bb6d-156">Evet</span><span class="sxs-lookup"><span data-stu-id="6bb6d-156">Yes</span></span> |
| <span data-ttu-id="6bb6d-157">password</span><span class="sxs-lookup"><span data-stu-id="6bb6d-157">password</span></span> |<span data-ttu-id="6bb6d-158">Belirttiğiniz hello kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-158">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="6bb6d-159">Evet</span><span class="sxs-lookup"><span data-stu-id="6bb6d-159">Yes</span></span> |
| <span data-ttu-id="6bb6d-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6bb6d-160">gatewayName</span></span> |<span data-ttu-id="6bb6d-161">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi MySQL veritabanına kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-161">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="6bb6d-162">Evet</span><span class="sxs-lookup"><span data-stu-id="6bb6d-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="6bb6d-163">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="6bb6d-163">Dataset properties</span></span>
<span data-ttu-id="6bb6d-164">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="6bb6d-165">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="6bb6d-166">Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="6bb6d-167">Merhaba typeProperties bölüm türü veri kümesi için **RelationalTable** hello aşağıdaki özelliklere sahip (MySQL dataset içerir)</span><span class="sxs-lookup"><span data-stu-id="6bb6d-167">hello typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has hello following properties</span></span>

| <span data-ttu-id="6bb6d-168">Özellik</span><span class="sxs-lookup"><span data-stu-id="6bb6d-168">Property</span></span> | <span data-ttu-id="6bb6d-169">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6bb6d-169">Description</span></span> | <span data-ttu-id="6bb6d-170">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6bb6d-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6bb6d-171">tableName</span><span class="sxs-lookup"><span data-stu-id="6bb6d-171">tableName</span></span> |<span data-ttu-id="6bb6d-172">Merhaba bağlı MySQL veritabanı örneğinde Merhaba tablonun adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-172">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="6bb6d-173">Hayır (varsa **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="6bb6d-173">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="6bb6d-174">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="6bb6d-174">Copy activity properties</span></span>
<span data-ttu-id="6bb6d-175">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6bb6d-176">Ad, açıklama, giriş ve çıkış tabloları gibi özellikleri olan ilkeleri etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-176">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="6bb6d-177">Oysa hello kullanılabilen özellikleri **typeProperties** hello etkinlik bölümünü her etkinlik türü ile değişir.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-177">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="6bb6d-178">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="6bb6d-179">Kopyalama etkinliği kaynağında türü olduğunda **RelationalSource** (içeren MySQL), aşağıdaki özelliklere hello typeProperties bölümünde bulunur:</span><span class="sxs-lookup"><span data-stu-id="6bb6d-179">When source in copy activity is of type **RelationalSource** (which includes MySQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="6bb6d-180">Özellik</span><span class="sxs-lookup"><span data-stu-id="6bb6d-180">Property</span></span> | <span data-ttu-id="6bb6d-181">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6bb6d-181">Description</span></span> | <span data-ttu-id="6bb6d-182">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="6bb6d-182">Allowed values</span></span> | <span data-ttu-id="6bb6d-183">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6bb6d-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6bb6d-184">sorgu</span><span class="sxs-lookup"><span data-stu-id="6bb6d-184">query</span></span> |<span data-ttu-id="6bb6d-185">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="6bb6d-186">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-186">SQL query string.</span></span> <span data-ttu-id="6bb6d-187">Örneğin: seçin * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-187">For example: select * from MyTable.</span></span> |<span data-ttu-id="6bb6d-188">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="6bb6d-188">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-tooazure-blob"></a><span data-ttu-id="6bb6d-189">JSON örnek: MySQL tooAzure Blob veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="6bb6d-189">JSON example: Copy data from MySQL tooAzure Blob</span></span>
<span data-ttu-id="6bb6d-190">Bu örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6bb6d-190">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="6bb6d-191">Bunu nasıl tooan Azure Blob Storage toocopy verilerden bir şirket içi MySQL veritabanı gösterir.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-191">It shows how toocopy data from an on-premises MySQL database tooan Azure Blob Storage.</span></span> <span data-ttu-id="6bb6d-192">Ancak, veri belirtildiği hello havuzlarını, kopyalanan tooany olabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-192">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6bb6d-193">Bu örnek, JSON parçacıklarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-193">This sample provides JSON snippets.</span></span> <span data-ttu-id="6bb6d-194">Merhaba veri fabrikası oluşturma için yönergeler içermez.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-194">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="6bb6d-195">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-195">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="6bb6d-196">Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="6bb6d-196">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="6bb6d-197">Bağlı hizmet türü [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6bb6d-197">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="6bb6d-198">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6bb6d-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="6bb6d-199">Bir giriş [dataset](data-factory-create-datasets.md) türü [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6bb6d-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="6bb6d-200">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6bb6d-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="6bb6d-201">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6bb6d-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="6bb6d-202">Merhaba örnek veri MySQL veritabanı tooa blob bir sorgu sonucunda saatlik kopyalar.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-202">hello sample copies data from a query result in MySQL database tooa blob hourly.</span></span> <span data-ttu-id="6bb6d-203">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-203">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="6bb6d-204">İlk adım olarak, hello veri yönetimi ağ geçidi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-204">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="6bb6d-205">Merhaba yönergelerdir hello [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-205">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="6bb6d-206">**MySQL hizmeti bağlı:**</span><span class="sxs-lookup"><span data-stu-id="6bb6d-206">**MySQL linked service:**</span></span>

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

<span data-ttu-id="6bb6d-207">**Azure Storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="6bb6d-207">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="6bb6d-208">**MySQL girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="6bb6d-208">**MySQL input dataset:**</span></span>

<span data-ttu-id="6bb6d-209">Merhaba örnek bir tablo "MyTable" MySQL içinde oluşturduğunuz ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-209">hello sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="6bb6d-210">"Dış" ayarı: "true" bildirir hello Data Factory hizmetinin bu hello tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-210">Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="6bb6d-211">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="6bb6d-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="6bb6d-212">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="6bb6d-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6bb6d-213">hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="6bb6d-214">Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="6bb6d-215">**Kopyalama etkinliği ile kanal:**</span><span class="sxs-lookup"><span data-stu-id="6bb6d-215">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="6bb6d-216">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-216">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="6bb6d-217">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**RelationalSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="6bb6d-218">Merhaba belirtilen hello SQL sorgusu **sorgu** özelliği saat toocopy geçmiş hello hello veri seçer.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="6bb6d-219">Tür eşlemesi için MySQL</span><span class="sxs-lookup"><span data-stu-id="6bb6d-219">Type mapping for MySQL</span></span>
<span data-ttu-id="6bb6d-220">Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri iki aşamalı bir yaklaşım aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="6bb6d-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="6bb6d-221">Yerel kaynak türleri too.NET türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="6bb6d-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="6bb6d-222">.NET türü toonative havuz türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="6bb6d-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="6bb6d-223">Veri tooMySQL taşırken hello aşağıdaki eşlemelerini MySQL türleri too.NET türlerinden kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-223">When moving data tooMySQL, hello following mappings are used from MySQL types too.NET types.</span></span>

| <span data-ttu-id="6bb6d-224">MySQL veritabanı türü</span><span class="sxs-lookup"><span data-stu-id="6bb6d-224">MySQL Database type</span></span> | <span data-ttu-id="6bb6d-225">.NET framework türü</span><span class="sxs-lookup"><span data-stu-id="6bb6d-225">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="6bb6d-226">bigint imzalanmamış</span><span class="sxs-lookup"><span data-stu-id="6bb6d-226">bigint unsigned</span></span> |<span data-ttu-id="6bb6d-227">Ondalık</span><span class="sxs-lookup"><span data-stu-id="6bb6d-227">Decimal</span></span> |
| <span data-ttu-id="6bb6d-228">bigint</span><span class="sxs-lookup"><span data-stu-id="6bb6d-228">bigint</span></span> |<span data-ttu-id="6bb6d-229">Int64</span><span class="sxs-lookup"><span data-stu-id="6bb6d-229">Int64</span></span> |
| <span data-ttu-id="6bb6d-230">bit</span><span class="sxs-lookup"><span data-stu-id="6bb6d-230">bit</span></span> |<span data-ttu-id="6bb6d-231">Ondalık</span><span class="sxs-lookup"><span data-stu-id="6bb6d-231">Decimal</span></span> |
| <span data-ttu-id="6bb6d-232">BLOB</span><span class="sxs-lookup"><span data-stu-id="6bb6d-232">blob</span></span> |<span data-ttu-id="6bb6d-233">Byte]</span><span class="sxs-lookup"><span data-stu-id="6bb6d-233">Byte[]</span></span> |
| <span data-ttu-id="6bb6d-234">bool</span><span class="sxs-lookup"><span data-stu-id="6bb6d-234">bool</span></span> |<span data-ttu-id="6bb6d-235">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="6bb6d-235">Boolean</span></span> |
| <span data-ttu-id="6bb6d-236">char</span><span class="sxs-lookup"><span data-stu-id="6bb6d-236">char</span></span> |<span data-ttu-id="6bb6d-237">Dize</span><span class="sxs-lookup"><span data-stu-id="6bb6d-237">String</span></span> |
| <span data-ttu-id="6bb6d-238">Tarih</span><span class="sxs-lookup"><span data-stu-id="6bb6d-238">date</span></span> |<span data-ttu-id="6bb6d-239">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="6bb6d-239">Datetime</span></span> |
| <span data-ttu-id="6bb6d-240">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="6bb6d-240">datetime</span></span> |<span data-ttu-id="6bb6d-241">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="6bb6d-241">Datetime</span></span> |
| <span data-ttu-id="6bb6d-242">Ondalık</span><span class="sxs-lookup"><span data-stu-id="6bb6d-242">decimal</span></span> |<span data-ttu-id="6bb6d-243">Ondalık</span><span class="sxs-lookup"><span data-stu-id="6bb6d-243">Decimal</span></span> |
| <span data-ttu-id="6bb6d-244">çift duyarlıklı</span><span class="sxs-lookup"><span data-stu-id="6bb6d-244">double precision</span></span> |<span data-ttu-id="6bb6d-245">Çift</span><span class="sxs-lookup"><span data-stu-id="6bb6d-245">Double</span></span> |
| <span data-ttu-id="6bb6d-246">Çift</span><span class="sxs-lookup"><span data-stu-id="6bb6d-246">double</span></span> |<span data-ttu-id="6bb6d-247">Çift</span><span class="sxs-lookup"><span data-stu-id="6bb6d-247">Double</span></span> |
| <span data-ttu-id="6bb6d-248">Enum</span><span class="sxs-lookup"><span data-stu-id="6bb6d-248">enum</span></span> |<span data-ttu-id="6bb6d-249">Dize</span><span class="sxs-lookup"><span data-stu-id="6bb6d-249">String</span></span> |
| <span data-ttu-id="6bb6d-250">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="6bb6d-250">float</span></span> |<span data-ttu-id="6bb6d-251">Tek</span><span class="sxs-lookup"><span data-stu-id="6bb6d-251">Single</span></span> |
| <span data-ttu-id="6bb6d-252">İmzasız int</span><span class="sxs-lookup"><span data-stu-id="6bb6d-252">int unsigned</span></span> |<span data-ttu-id="6bb6d-253">Int64</span><span class="sxs-lookup"><span data-stu-id="6bb6d-253">Int64</span></span> |
| <span data-ttu-id="6bb6d-254">Int</span><span class="sxs-lookup"><span data-stu-id="6bb6d-254">int</span></span> |<span data-ttu-id="6bb6d-255">Int32</span><span class="sxs-lookup"><span data-stu-id="6bb6d-255">Int32</span></span> |
| <span data-ttu-id="6bb6d-256">işaretsiz tamsayı</span><span class="sxs-lookup"><span data-stu-id="6bb6d-256">integer unsigned</span></span> |<span data-ttu-id="6bb6d-257">Int64</span><span class="sxs-lookup"><span data-stu-id="6bb6d-257">Int64</span></span> |
| <span data-ttu-id="6bb6d-258">tamsayı</span><span class="sxs-lookup"><span data-stu-id="6bb6d-258">integer</span></span> |<span data-ttu-id="6bb6d-259">Int32</span><span class="sxs-lookup"><span data-stu-id="6bb6d-259">Int32</span></span> |
| <span data-ttu-id="6bb6d-260">uzun varbinary</span><span class="sxs-lookup"><span data-stu-id="6bb6d-260">long varbinary</span></span> |<span data-ttu-id="6bb6d-261">Byte]</span><span class="sxs-lookup"><span data-stu-id="6bb6d-261">Byte[]</span></span> |
| <span data-ttu-id="6bb6d-262">uzun varchar</span><span class="sxs-lookup"><span data-stu-id="6bb6d-262">long varchar</span></span> |<span data-ttu-id="6bb6d-263">Dize</span><span class="sxs-lookup"><span data-stu-id="6bb6d-263">String</span></span> |
| <span data-ttu-id="6bb6d-264">longblob</span><span class="sxs-lookup"><span data-stu-id="6bb6d-264">longblob</span></span> |<span data-ttu-id="6bb6d-265">Byte]</span><span class="sxs-lookup"><span data-stu-id="6bb6d-265">Byte[]</span></span> |
| <span data-ttu-id="6bb6d-266">LONGTEXT</span><span class="sxs-lookup"><span data-stu-id="6bb6d-266">longtext</span></span> |<span data-ttu-id="6bb6d-267">Dize</span><span class="sxs-lookup"><span data-stu-id="6bb6d-267">String</span></span> |
| <span data-ttu-id="6bb6d-268">mediumblob</span><span class="sxs-lookup"><span data-stu-id="6bb6d-268">mediumblob</span></span> |<span data-ttu-id="6bb6d-269">Byte]</span><span class="sxs-lookup"><span data-stu-id="6bb6d-269">Byte[]</span></span> |
| <span data-ttu-id="6bb6d-270">İmzasız mediumint</span><span class="sxs-lookup"><span data-stu-id="6bb6d-270">mediumint unsigned</span></span> |<span data-ttu-id="6bb6d-271">Int64</span><span class="sxs-lookup"><span data-stu-id="6bb6d-271">Int64</span></span> |
| <span data-ttu-id="6bb6d-272">mediumint</span><span class="sxs-lookup"><span data-stu-id="6bb6d-272">mediumint</span></span> |<span data-ttu-id="6bb6d-273">Int32</span><span class="sxs-lookup"><span data-stu-id="6bb6d-273">Int32</span></span> |
| <span data-ttu-id="6bb6d-274">mediumtext</span><span class="sxs-lookup"><span data-stu-id="6bb6d-274">mediumtext</span></span> |<span data-ttu-id="6bb6d-275">Dize</span><span class="sxs-lookup"><span data-stu-id="6bb6d-275">String</span></span> |
| <span data-ttu-id="6bb6d-276">sayısal</span><span class="sxs-lookup"><span data-stu-id="6bb6d-276">numeric</span></span> |<span data-ttu-id="6bb6d-277">Ondalık</span><span class="sxs-lookup"><span data-stu-id="6bb6d-277">Decimal</span></span> |
| <span data-ttu-id="6bb6d-278">Gerçek</span><span class="sxs-lookup"><span data-stu-id="6bb6d-278">real</span></span> |<span data-ttu-id="6bb6d-279">Çift</span><span class="sxs-lookup"><span data-stu-id="6bb6d-279">Double</span></span> |
| <span data-ttu-id="6bb6d-280">ayarlama</span><span class="sxs-lookup"><span data-stu-id="6bb6d-280">set</span></span> |<span data-ttu-id="6bb6d-281">Dize</span><span class="sxs-lookup"><span data-stu-id="6bb6d-281">String</span></span> |
| <span data-ttu-id="6bb6d-282">işaretsiz tamsayı</span><span class="sxs-lookup"><span data-stu-id="6bb6d-282">smallint unsigned</span></span> |<span data-ttu-id="6bb6d-283">Int32</span><span class="sxs-lookup"><span data-stu-id="6bb6d-283">Int32</span></span> |
| <span data-ttu-id="6bb6d-284">tamsayı</span><span class="sxs-lookup"><span data-stu-id="6bb6d-284">smallint</span></span> |<span data-ttu-id="6bb6d-285">Int16</span><span class="sxs-lookup"><span data-stu-id="6bb6d-285">Int16</span></span> |
| <span data-ttu-id="6bb6d-286">Metin</span><span class="sxs-lookup"><span data-stu-id="6bb6d-286">text</span></span> |<span data-ttu-id="6bb6d-287">Dize</span><span class="sxs-lookup"><span data-stu-id="6bb6d-287">String</span></span> |
| <span data-ttu-id="6bb6d-288">time</span><span class="sxs-lookup"><span data-stu-id="6bb6d-288">time</span></span> |<span data-ttu-id="6bb6d-289">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6bb6d-289">TimeSpan</span></span> |
| <span data-ttu-id="6bb6d-290">timestamp</span><span class="sxs-lookup"><span data-stu-id="6bb6d-290">timestamp</span></span> |<span data-ttu-id="6bb6d-291">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="6bb6d-291">Datetime</span></span> |
| <span data-ttu-id="6bb6d-292">tinyblob</span><span class="sxs-lookup"><span data-stu-id="6bb6d-292">tinyblob</span></span> |<span data-ttu-id="6bb6d-293">Byte]</span><span class="sxs-lookup"><span data-stu-id="6bb6d-293">Byte[]</span></span> |
| <span data-ttu-id="6bb6d-294">İmzasız tinyint</span><span class="sxs-lookup"><span data-stu-id="6bb6d-294">tinyint unsigned</span></span> |<span data-ttu-id="6bb6d-295">Int16</span><span class="sxs-lookup"><span data-stu-id="6bb6d-295">Int16</span></span> |
| <span data-ttu-id="6bb6d-296">Mini tamsayı</span><span class="sxs-lookup"><span data-stu-id="6bb6d-296">tinyint</span></span> |<span data-ttu-id="6bb6d-297">Int16</span><span class="sxs-lookup"><span data-stu-id="6bb6d-297">Int16</span></span> |
| <span data-ttu-id="6bb6d-298">tinytext</span><span class="sxs-lookup"><span data-stu-id="6bb6d-298">tinytext</span></span> |<span data-ttu-id="6bb6d-299">Dize</span><span class="sxs-lookup"><span data-stu-id="6bb6d-299">String</span></span> |
| <span data-ttu-id="6bb6d-300">varchar</span><span class="sxs-lookup"><span data-stu-id="6bb6d-300">varchar</span></span> |<span data-ttu-id="6bb6d-301">Dize</span><span class="sxs-lookup"><span data-stu-id="6bb6d-301">String</span></span> |
| <span data-ttu-id="6bb6d-302">Yıl</span><span class="sxs-lookup"><span data-stu-id="6bb6d-302">year</span></span> |<span data-ttu-id="6bb6d-303">Int</span><span class="sxs-lookup"><span data-stu-id="6bb6d-303">Int</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="6bb6d-304">Kaynak toosink sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="6bb6d-304">Map source toosink columns</span></span>
<span data-ttu-id="6bb6d-305">Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="6bb6d-305">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="6bb6d-306">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="6bb6d-306">Repeatable read from relational sources</span></span>
<span data-ttu-id="6bb6d-307">İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-307">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="6bb6d-308">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-308">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="6bb6d-309">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-309">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="6bb6d-310">Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-310">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="6bb6d-311">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="6bb6d-311">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="6bb6d-312">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="6bb6d-312">Performance and Tuning</span></span>
<span data-ttu-id="6bb6d-313">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="6bb6d-313">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
