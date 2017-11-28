---
title: Azure Data Factory kullanarak Sybase aaaMove verilerden | Microsoft Docs
description: "Hakkında bilgi edinin Azure Data Factory kullanarak Sybase veritabanından toomove veri."
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
ms.openlocfilehash: ad003ec502028d56db9570fe08af329eb5b71817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="7c87c-103">Azure Data Factory kullanarak Sybase taşıma verileri</span><span class="sxs-lookup"><span data-stu-id="7c87c-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="7c87c-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri bir şirket içi Sybase veritabanından açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7c87c-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Sybase database.</span></span> <span data-ttu-id="7c87c-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="7c87c-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="7c87c-106">Bir şirket içi Sybase veri deposu desteklenen tooany havuz veri deposundan verileri kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c87c-106">You can copy data from an on-premises Sybase data store tooany supported sink data store.</span></span> <span data-ttu-id="7c87c-107">Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="7c87c-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="7c87c-108">Veri Fabrikası şu anda verileri Sybase verilerinden tooother veri depolarına depolamak taşıma yalnızca, ancak diğer veri depoları tooa Sybase veri deposundan veri taşıma değil destekler.</span><span class="sxs-lookup"><span data-stu-id="7c87c-108">Data factory currently supports only moving data from a Sybase data store tooother data stores, but not for moving data from other data stores tooa Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7c87c-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7c87c-109">Prerequisites</span></span>
<span data-ttu-id="7c87c-110">Data Factory Hizmeti'ne hello veri yönetimi ağ geçidi kullanarak bağlanan tooon içi Sybase kaynakları destekler.</span><span class="sxs-lookup"><span data-stu-id="7c87c-110">Data Factory service supports connecting tooon-premises Sybase sources using hello Data Management Gateway.</span></span> <span data-ttu-id="7c87c-111">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale toolearn veri yönetimi ağ geçidi ve hello ağ geçidi kurun ayarlama hakkında adım adım yönergeleri hakkında.</span><span class="sxs-lookup"><span data-stu-id="7c87c-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="7c87c-112">Bir Azure Iaas sanal Hello Sybase veritabanını barındıran olsa bile ağ geçidi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7c87c-112">Gateway is required even if hello Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="7c87c-113">Merhaba ağ geçidi üzerinde aynı Iaas VM hello veri olarak depolamak veya hello ağ geçidi olarak aynı uzunlukta farklı bir VM üzerinde toohello veritabanı bağlanabilir hello yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c87c-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="7c87c-114">Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="7c87c-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="7c87c-115">Desteklenen sürümleri ve yükleme</span><span class="sxs-lookup"><span data-stu-id="7c87c-115">Supported versions and installation</span></span>
<span data-ttu-id="7c87c-116">Veri Yönetimi ağ geçidi tooconnect toohello Sybase veritabanı için ihtiyacınız tooinstall hello [Sybase iAnywhere.Data.SQLAnywhere için veri sağlayıcı](http://go.microsoft.com/fwlink/?linkid=324846) 16 veya yukarıdaki üzerinde aynı hello veri yönetimi ağ geçidi hello gibi sistem.</span><span class="sxs-lookup"><span data-stu-id="7c87c-116">For Data Management Gateway tooconnect toohello Sybase Database, you need tooinstall hello [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="7c87c-117">Sybase sürüm 16 ve üzeri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="7c87c-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="7c87c-118">Başlarken</span><span class="sxs-lookup"><span data-stu-id="7c87c-118">Getting started</span></span>
<span data-ttu-id="7c87c-119">Farklı araçlar/API'lerini kullanarak bir şirket içi Cassandra veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7c87c-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="7c87c-120">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="7c87c-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="7c87c-121">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="7c87c-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="7c87c-122">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="7c87c-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="7c87c-123">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="7c87c-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="7c87c-124">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7c87c-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="7c87c-125">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="7c87c-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="7c87c-126">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="7c87c-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="7c87c-127">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="7c87c-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="7c87c-128">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7c87c-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="7c87c-129">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="7c87c-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="7c87c-130">Bir şirket içi Sybase veri deposundaki kullanılan toocopy verileri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: Blob Sybase tooAzure veri kopyalama](#json-example-copy-data-from-sybase-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="7c87c-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase tooAzure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="7c87c-131">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooa Sybase veri deposu olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="7c87c-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="7c87c-132">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="7c87c-132">Linked service properties</span></span>
<span data-ttu-id="7c87c-133">Aşağıdaki tablonun hello JSON öğeleri belirli tooSybase bağlantılı hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c87c-133">hello following table provides description for JSON elements specific tooSybase linked service.</span></span>

| <span data-ttu-id="7c87c-134">Özellik</span><span class="sxs-lookup"><span data-stu-id="7c87c-134">Property</span></span> | <span data-ttu-id="7c87c-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7c87c-135">Description</span></span> | <span data-ttu-id="7c87c-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7c87c-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7c87c-137">type</span><span class="sxs-lookup"><span data-stu-id="7c87c-137">type</span></span> |<span data-ttu-id="7c87c-138">Merhaba type özelliği ayarlanmalıdır: **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="7c87c-138">hello type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="7c87c-139">Evet</span><span class="sxs-lookup"><span data-stu-id="7c87c-139">Yes</span></span> |
| <span data-ttu-id="7c87c-140">sunucu</span><span class="sxs-lookup"><span data-stu-id="7c87c-140">server</span></span> |<span data-ttu-id="7c87c-141">Merhaba Sybase sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="7c87c-141">Name of hello Sybase server.</span></span> |<span data-ttu-id="7c87c-142">Evet</span><span class="sxs-lookup"><span data-stu-id="7c87c-142">Yes</span></span> |
| <span data-ttu-id="7c87c-143">Veritabanı</span><span class="sxs-lookup"><span data-stu-id="7c87c-143">database</span></span> |<span data-ttu-id="7c87c-144">Merhaba Sybase veritabanının adı.</span><span class="sxs-lookup"><span data-stu-id="7c87c-144">Name of hello Sybase database.</span></span> |<span data-ttu-id="7c87c-145">Evet</span><span class="sxs-lookup"><span data-stu-id="7c87c-145">Yes</span></span> |
| <span data-ttu-id="7c87c-146">Şema</span><span class="sxs-lookup"><span data-stu-id="7c87c-146">schema</span></span> |<span data-ttu-id="7c87c-147">Merhaba veritabanındaki hello şema adı.</span><span class="sxs-lookup"><span data-stu-id="7c87c-147">Name of hello schema in hello database.</span></span> |<span data-ttu-id="7c87c-148">Hayır</span><span class="sxs-lookup"><span data-stu-id="7c87c-148">No</span></span> |
| <span data-ttu-id="7c87c-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="7c87c-149">authenticationType</span></span> |<span data-ttu-id="7c87c-150">Kimlik doğrulama türü tooconnect toohello Sybase veritabanına kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7c87c-150">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="7c87c-151">Olası değerler şunlardır: Anonim, temel ve Windows.</span><span class="sxs-lookup"><span data-stu-id="7c87c-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="7c87c-152">Evet</span><span class="sxs-lookup"><span data-stu-id="7c87c-152">Yes</span></span> |
| <span data-ttu-id="7c87c-153">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="7c87c-153">username</span></span> |<span data-ttu-id="7c87c-154">Temel veya Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="7c87c-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="7c87c-155">Hayır</span><span class="sxs-lookup"><span data-stu-id="7c87c-155">No</span></span> |
| <span data-ttu-id="7c87c-156">password</span><span class="sxs-lookup"><span data-stu-id="7c87c-156">password</span></span> |<span data-ttu-id="7c87c-157">Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="7c87c-157">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="7c87c-158">Hayır</span><span class="sxs-lookup"><span data-stu-id="7c87c-158">No</span></span> |
| <span data-ttu-id="7c87c-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="7c87c-159">gatewayName</span></span> |<span data-ttu-id="7c87c-160">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi Sybase veritabanına kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c87c-160">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="7c87c-161">Evet</span><span class="sxs-lookup"><span data-stu-id="7c87c-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="7c87c-162">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="7c87c-162">Dataset properties</span></span>
<span data-ttu-id="7c87c-163">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="7c87c-163">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="7c87c-164">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="7c87c-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="7c87c-165">Merhaba typeProperties bölümü veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c87c-165">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="7c87c-166">Merhaba **typeProperties** veri kümesi için bir bölüm türü **RelationalTable** (Sybase veri kümesi içeren) hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="7c87c-166">hello **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has hello following properties:</span></span>

| <span data-ttu-id="7c87c-167">Özellik</span><span class="sxs-lookup"><span data-stu-id="7c87c-167">Property</span></span> | <span data-ttu-id="7c87c-168">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7c87c-168">Description</span></span> | <span data-ttu-id="7c87c-169">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7c87c-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7c87c-170">tableName</span><span class="sxs-lookup"><span data-stu-id="7c87c-170">tableName</span></span> |<span data-ttu-id="7c87c-171">Merhaba bağlı Sybase veritabanı örneğinde Merhaba tablonun adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7c87c-171">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="7c87c-172">Hayır (varsa **sorgu** , **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="7c87c-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="7c87c-173">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="7c87c-173">Copy activity properties</span></span>
<span data-ttu-id="7c87c-174">Bölümler & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz: [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="7c87c-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7c87c-175">Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7c87c-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="7c87c-176">Oysa hello typeProperties bölümünde hello etkinlik özellikleri her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="7c87c-176">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="7c87c-177">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="7c87c-177">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="7c87c-178">Merhaba kaynak türü olduğunda **RelationalSource** (içeren Sybase), aşağıdaki özelliklere hello kullanılabilir **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="7c87c-178">When hello source is of type **RelationalSource** (which includes Sybase), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="7c87c-179">Özellik</span><span class="sxs-lookup"><span data-stu-id="7c87c-179">Property</span></span> | <span data-ttu-id="7c87c-180">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7c87c-180">Description</span></span> | <span data-ttu-id="7c87c-181">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="7c87c-181">Allowed values</span></span> | <span data-ttu-id="7c87c-182">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7c87c-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7c87c-183">sorgu</span><span class="sxs-lookup"><span data-stu-id="7c87c-183">query</span></span> |<span data-ttu-id="7c87c-184">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="7c87c-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="7c87c-185">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="7c87c-185">SQL query string.</span></span> <span data-ttu-id="7c87c-186">Örneğin: seçin * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="7c87c-186">For example: select * from MyTable.</span></span> |<span data-ttu-id="7c87c-187">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="7c87c-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-tooazure-blob"></a><span data-ttu-id="7c87c-188">JSON örnek: Blob Sybase tooAzure veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="7c87c-188">JSON example: Copy data from Sybase tooAzure Blob</span></span>
<span data-ttu-id="7c87c-189">Merhaba aşağıdaki örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7c87c-189">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="7c87c-190">Bunlar, Sybase toocopy verileri tooAzure Blob Storage nasıl veritabanı gösterir.</span><span class="sxs-lookup"><span data-stu-id="7c87c-190">They show how toocopy data from Sybase database tooAzure Blob Storage.</span></span> <span data-ttu-id="7c87c-191">Ancak, veri belirtildiği hello havuzlarını, kopyalanan tooany olabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="7c87c-191">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="7c87c-192">Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="7c87c-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="7c87c-193">Bağlı hizmet türü [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7c87c-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="7c87c-194">Türünde bir liked hizmet [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="7c87c-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="7c87c-195">Bir giriş [dataset](data-factory-create-datasets.md) türü [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7c87c-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="7c87c-196">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7c87c-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="7c87c-197">Merhaba [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="7c87c-197">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="7c87c-198">Merhaba örnek veri Sybase veritabanı tooa blob bir sorgu sonucunda her saat kopyalar.</span><span class="sxs-lookup"><span data-stu-id="7c87c-198">hello sample copies data from a query result in Sybase database tooa blob every hour.</span></span> <span data-ttu-id="7c87c-199">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="7c87c-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="7c87c-200">İlk adım olarak, hello veri yönetimi ağ geçidi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7c87c-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="7c87c-201">Merhaba yönergelerdir hello [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="7c87c-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="7c87c-202">**Sybase bağlantılı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="7c87c-202">**Sybase linked service:**</span></span>

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

<span data-ttu-id="7c87c-203">**Azure Blob storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="7c87c-203">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="7c87c-204">**Sybase girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="7c87c-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="7c87c-205">Merhaba örnek bir tablo "MyTable" Sybase içinde oluşturduğunuz ve zaman serisi veri için "zaman damgası" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="7c87c-205">hello sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="7c87c-206">"Dış" ayarı: true, bu veri kümesi dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil hello Data Factory hizmetinin bildirir.</span><span class="sxs-lookup"><span data-stu-id="7c87c-206">Setting “external”: true informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="7c87c-207">Bu hello fark **türü** Merhaba bağlantılı hizmet ayarlanır: **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="7c87c-207">Notice that hello **type** of hello linked service is set to: **RelationalTable**.</span></span>

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

<span data-ttu-id="7c87c-208">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="7c87c-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="7c87c-209">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="7c87c-209">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="7c87c-210">hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="7c87c-210">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="7c87c-211">Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="7c87c-211">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="7c87c-212">**Kopyalama etkinliği ile kanal:**</span><span class="sxs-lookup"><span data-stu-id="7c87c-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="7c87c-213">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun saatlik ise.</span><span class="sxs-lookup"><span data-stu-id="7c87c-213">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="7c87c-214">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**RelationalSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="7c87c-214">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="7c87c-215">Merhaba belirtilen hello SQL sorgusu **sorgu** özelliği DBA hello hello veri seçer. Merhaba veritabanındaki Siparişler tablosu.</span><span class="sxs-lookup"><span data-stu-id="7c87c-215">hello SQL query specified for hello **query** property selects hello data from hello DBA.Orders table in hello database.</span></span>

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

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="7c87c-216">Sybase için tür eşlemesi</span><span class="sxs-lookup"><span data-stu-id="7c87c-216">Type mapping for Sybase</span></span>
<span data-ttu-id="7c87c-217">Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, hello kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri 2 adımlı yaklaşımı izleyerek hello ile:</span><span class="sxs-lookup"><span data-stu-id="7c87c-217">As mentioned in hello [Data Movement Activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="7c87c-218">Yerel kaynak türleri too.NET türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="7c87c-218">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="7c87c-219">.NET türü toonative havuz türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="7c87c-219">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="7c87c-220">Sybase T-SQL ve T-SQL türlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="7c87c-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="7c87c-221">Sql türleri too.NET türünden bir eşleme tablo için bkz: [Azure SQL Bağlayıcısı](data-factory-azure-sql-connector.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="7c87c-221">For a mapping table from sql types too.NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="7c87c-222">Kaynak toosink sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="7c87c-222">Map source toosink columns</span></span>
<span data-ttu-id="7c87c-223">Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="7c87c-223">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="7c87c-224">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="7c87c-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="7c87c-225">İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları.</span><span class="sxs-lookup"><span data-stu-id="7c87c-225">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="7c87c-226">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c87c-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="7c87c-227">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c87c-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="7c87c-228">Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7c87c-228">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="7c87c-229">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="7c87c-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="7c87c-230">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="7c87c-230">Performance and Tuning</span></span>
<span data-ttu-id="7c87c-231">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="7c87c-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
