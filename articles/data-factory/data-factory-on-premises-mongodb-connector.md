---
title: Data Factory kullanarak MongoDB aaaMove verilerden | Microsoft Docs
description: "Azure Data Factory kullanarak MongoDB toomove verileri nasıl veritabanı hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a><span data-ttu-id="565ed-103">Azure Data Factory kullanarak MongoDB gelen veri taşıma</span><span class="sxs-lookup"><span data-stu-id="565ed-103">Move data From MongoDB using Azure Data Factory</span></span>
<span data-ttu-id="565ed-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri bir şirket içi MongoDB veritabanından açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="565ed-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MongoDB database.</span></span> <span data-ttu-id="565ed-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="565ed-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="565ed-106">Bir şirket içi MongoDB veri deposu desteklenen tooany havuz veri deposundan verileri kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="565ed-106">You can copy data from an on-premises MongoDB data store tooany supported sink data store.</span></span> <span data-ttu-id="565ed-107">Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="565ed-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="565ed-108">Veri Fabrikası şu anda verileri MongoDB verilerinden tooother veri depolarına depolamak taşıma yalnızca, ancak diğer veri depoları tooan MongoDB deposundan veri taşıma değil destekler.</span><span class="sxs-lookup"><span data-stu-id="565ed-108">Data factory currently supports only moving data from a MongoDB data store tooother data stores, but not for moving data from other data stores tooan MongoDB datastore.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="565ed-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="565ed-109">Prerequisites</span></span>
<span data-ttu-id="565ed-110">Hello Azure Data Factory hizmeti toobe mümkün tooconnect tooyour şirket içi MongoDB veritabanı için aşağıdaki bileşenleri hello yüklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="565ed-110">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises MongoDB database, you must install hello following components:</span></span>

- <span data-ttu-id="565ed-111">Desteklenmeyen MongoDB sürümler: 2.4, 2.6, 3.0 ve 3.2.</span><span class="sxs-lookup"><span data-stu-id="565ed-111">Supported MongoDB versions are:  2.4, 2.6, 3.0, and 3.2.</span></span>
- <span data-ttu-id="565ed-112">Veri Yönetimi ağ geçidi ana hello veritabanının aynı makine hello veya hello veritabanıyla kaynakları için rekabete ayrı makine tooavoid.</span><span class="sxs-lookup"><span data-stu-id="565ed-112">Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="565ed-113">Veri Yönetimi ağ geçidi, şirket içi veri kaynakları toocloud Hizmetleri güvenli ve yönetilen bir şekilde birbirine bağlayan bir yazılımdır.</span><span class="sxs-lookup"><span data-stu-id="565ed-113">Data Management Gateway is a software that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="565ed-114">Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) makale veri yönetimi ağ geçidi hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="565ed-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="565ed-115">Bkz: [şirket içi toocloud veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale hello ağ geçidi veri ardışık düzen toomove veri ayarlama hakkında adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="565ed-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

    <span data-ttu-id="565ed-116">Merhaba ağ geçidi yüklediğinizde, bir Microsoft MongoDB ODBC sürücüsü kullanılan tooconnect tooMongoDB otomatik olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="565ed-116">When you install hello gateway, it automatically installs a Microsoft MongoDB ODBC driver used tooconnect tooMongoDB.</span></span>

    > [!NOTE]
    > <span data-ttu-id="565ed-117">Azure Iaas Vm'lerde barındırılan olsa bile toouse hello ağ geçidi tooconnect tooMongoDB gerekir.</span><span class="sxs-lookup"><span data-stu-id="565ed-117">You need toouse hello gateway tooconnect tooMongoDB even if it is hosted in Azure IaaS VMs.</span></span> <span data-ttu-id="565ed-118">Bulutta barındırılan MongoDB tooconnect tooan örneğini çalışıyorsanız, hello ağ geçidi örneği hello Iaas VM yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="565ed-118">If you are trying tooconnect tooan instance of MongoDB hosted in cloud, you can also install hello gateway instance in hello IaaS VM.</span></span>

## <a name="getting-started"></a><span data-ttu-id="565ed-119">Başlarken</span><span class="sxs-lookup"><span data-stu-id="565ed-119">Getting started</span></span>
<span data-ttu-id="565ed-120">Farklı araçlar/API'lerini kullanarak bir şirket içi MongoDB veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="565ed-120">You can create a pipeline with a copy activity that moves data from an on-premises MongoDB data store by using different tools/APIs.</span></span>

<span data-ttu-id="565ed-121">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="565ed-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="565ed-122">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="565ed-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="565ed-123">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="565ed-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="565ed-124">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="565ed-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="565ed-125">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="565ed-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="565ed-126">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="565ed-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="565ed-127">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="565ed-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="565ed-128">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="565ed-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="565ed-129">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="565ed-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="565ed-130">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="565ed-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="565ed-131">Bir şirket içi MongoDB veri deposundaki kullanılan toocopy verileri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: MongoDB tooAzure Blob veri kopyalama](#json-example-copy-data-from-mongodb-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="565ed-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MongoDB data store, see [JSON example: Copy data from MongoDB tooAzure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="565ed-132">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooMongoDB kaynağı JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="565ed-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooMongoDB source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="565ed-133">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="565ed-133">Linked service properties</span></span>
<span data-ttu-id="565ed-134">Merhaba aşağıdaki tabloda JSON öğeleri belirli açıklamasını çok sağlar**OnPremisesMongoDB** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="565ed-134">hello following table provides description for JSON elements specific too**OnPremisesMongoDB** linked service.</span></span>

| <span data-ttu-id="565ed-135">Özellik</span><span class="sxs-lookup"><span data-stu-id="565ed-135">Property</span></span> | <span data-ttu-id="565ed-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="565ed-136">Description</span></span> | <span data-ttu-id="565ed-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="565ed-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="565ed-138">type</span><span class="sxs-lookup"><span data-stu-id="565ed-138">type</span></span> |<span data-ttu-id="565ed-139">Merhaba type özelliği ayarlanmalıdır: **OnPremisesMongoDb**</span><span class="sxs-lookup"><span data-stu-id="565ed-139">hello type property must be set to: **OnPremisesMongoDb**</span></span> |<span data-ttu-id="565ed-140">Evet</span><span class="sxs-lookup"><span data-stu-id="565ed-140">Yes</span></span> |
| <span data-ttu-id="565ed-141">sunucu</span><span class="sxs-lookup"><span data-stu-id="565ed-141">server</span></span> |<span data-ttu-id="565ed-142">IP adresi veya ana bilgisayar hello MongoDB sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="565ed-142">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="565ed-143">Evet</span><span class="sxs-lookup"><span data-stu-id="565ed-143">Yes</span></span> |
| <span data-ttu-id="565ed-144">port</span><span class="sxs-lookup"><span data-stu-id="565ed-144">port</span></span> |<span data-ttu-id="565ed-145">MongoDB sunucusuna hello TCP bağlantı noktası toolisten istemci bağlantıları için kullanır.</span><span class="sxs-lookup"><span data-stu-id="565ed-145">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="565ed-146">İsteğe bağlı, varsayılan değer: 27017</span><span class="sxs-lookup"><span data-stu-id="565ed-146">Optional, default value: 27017</span></span> |
| <span data-ttu-id="565ed-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="565ed-147">authenticationType</span></span> |<span data-ttu-id="565ed-148">Basic veya Anonymous.</span><span class="sxs-lookup"><span data-stu-id="565ed-148">Basic, or Anonymous.</span></span> |<span data-ttu-id="565ed-149">Evet</span><span class="sxs-lookup"><span data-stu-id="565ed-149">Yes</span></span> |
| <span data-ttu-id="565ed-150">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="565ed-150">username</span></span> |<span data-ttu-id="565ed-151">Kullanıcı hesabı tooaccess MongoDB.</span><span class="sxs-lookup"><span data-stu-id="565ed-151">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="565ed-152">Evet (Temel kimlik doğrulaması kullanılıyorsa).</span><span class="sxs-lookup"><span data-stu-id="565ed-152">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="565ed-153">password</span><span class="sxs-lookup"><span data-stu-id="565ed-153">password</span></span> |<span data-ttu-id="565ed-154">Merhaba kullanıcının parolası.</span><span class="sxs-lookup"><span data-stu-id="565ed-154">Password for hello user.</span></span> |<span data-ttu-id="565ed-155">Evet (Temel kimlik doğrulaması kullanılıyorsa).</span><span class="sxs-lookup"><span data-stu-id="565ed-155">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="565ed-156">authSource</span><span class="sxs-lookup"><span data-stu-id="565ed-156">authSource</span></span> |<span data-ttu-id="565ed-157">Kimlik doğrulaması için kimlik bilgilerinizi toouse toocheck istediğiniz hello MongoDB veritabanı adı.</span><span class="sxs-lookup"><span data-stu-id="565ed-157">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="565ed-158">(Temel kimlik doğrulaması kullanılıyorsa) isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="565ed-158">Optional (if basic authentication is used).</span></span> <span data-ttu-id="565ed-159">Varsayılan: Merhaba yönetici hesabı ve databaseName özelliği kullanılarak belirtilen hello veritabanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="565ed-159">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="565ed-160">databaseName</span><span class="sxs-lookup"><span data-stu-id="565ed-160">databaseName</span></span> |<span data-ttu-id="565ed-161">Tooaccess istediğiniz hello MongoDB veritabanı adı.</span><span class="sxs-lookup"><span data-stu-id="565ed-161">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="565ed-162">Evet</span><span class="sxs-lookup"><span data-stu-id="565ed-162">Yes</span></span> |
| <span data-ttu-id="565ed-163">gatewayName</span><span class="sxs-lookup"><span data-stu-id="565ed-163">gatewayName</span></span> |<span data-ttu-id="565ed-164">Merhaba veri deposu erişen hello ağ geçidi adı.</span><span class="sxs-lookup"><span data-stu-id="565ed-164">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="565ed-165">Evet</span><span class="sxs-lookup"><span data-stu-id="565ed-165">Yes</span></span> |
| <span data-ttu-id="565ed-166">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="565ed-166">encryptedCredential</span></span> |<span data-ttu-id="565ed-167">Ağ Geçidi tarafından şifrelenmiş kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="565ed-167">Credential encrypted by gateway.</span></span> |<span data-ttu-id="565ed-168">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="565ed-168">Optional</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="565ed-169">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="565ed-169">Dataset properties</span></span>
<span data-ttu-id="565ed-170">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="565ed-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="565ed-171">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="565ed-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="565ed-172">Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="565ed-172">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="565ed-173">Merhaba typeProperties bölüm türü veri kümesi için **MongoDbCollection** hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="565ed-173">hello typeProperties section for dataset of type **MongoDbCollection** has hello following properties:</span></span>

| <span data-ttu-id="565ed-174">Özellik</span><span class="sxs-lookup"><span data-stu-id="565ed-174">Property</span></span> | <span data-ttu-id="565ed-175">Açıklama</span><span class="sxs-lookup"><span data-stu-id="565ed-175">Description</span></span> | <span data-ttu-id="565ed-176">Gerekli</span><span class="sxs-lookup"><span data-stu-id="565ed-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="565ed-177">collectionName</span><span class="sxs-lookup"><span data-stu-id="565ed-177">collectionName</span></span> |<span data-ttu-id="565ed-178">MongoDB veritabanı hello koleksiyonunda adı.</span><span class="sxs-lookup"><span data-stu-id="565ed-178">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="565ed-179">Evet</span><span class="sxs-lookup"><span data-stu-id="565ed-179">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="565ed-180">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="565ed-180">Copy activity properties</span></span>
<span data-ttu-id="565ed-181">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="565ed-181">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="565ed-182">Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="565ed-182">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="565ed-183">Hello kullanılabilen özellikleri **typeProperties** bölüm diğer yandan hello hello faaliyete, her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="565ed-183">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="565ed-184">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="565ed-184">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="565ed-185">Merhaba kaynak türü olduğunda **MongoDbSource** aşağıdaki özelliklere hello typeProperties bölümünde bulunur:</span><span class="sxs-lookup"><span data-stu-id="565ed-185">When hello source is of type **MongoDbSource** hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="565ed-186">Özellik</span><span class="sxs-lookup"><span data-stu-id="565ed-186">Property</span></span> | <span data-ttu-id="565ed-187">Açıklama</span><span class="sxs-lookup"><span data-stu-id="565ed-187">Description</span></span> | <span data-ttu-id="565ed-188">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="565ed-188">Allowed values</span></span> | <span data-ttu-id="565ed-189">Gerekli</span><span class="sxs-lookup"><span data-stu-id="565ed-189">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="565ed-190">sorgu</span><span class="sxs-lookup"><span data-stu-id="565ed-190">query</span></span> |<span data-ttu-id="565ed-191">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="565ed-191">Use hello custom query tooread data.</span></span> |<span data-ttu-id="565ed-192">SQL-92 sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="565ed-192">SQL-92 query string.</span></span> <span data-ttu-id="565ed-193">Örneğin: seçin * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="565ed-193">For example: select * from MyTable.</span></span> |<span data-ttu-id="565ed-194">Hayır (varsa **collectionName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="565ed-194">No (if **collectionName** of **dataset** is specified)</span></span> |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a><span data-ttu-id="565ed-195">JSON örnek: MongoDB tooAzure Blob veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="565ed-195">JSON example: Copy data from MongoDB tooAzure Blob</span></span>
<span data-ttu-id="565ed-196">Bu örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="565ed-196">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="565ed-197">Bunu gösterir nasıl bir şirket içi MongoDB tooan Azure Blob Storage toocopy verileri.</span><span class="sxs-lookup"><span data-stu-id="565ed-197">It shows how toocopy data from an on-premises MongoDB tooan Azure Blob Storage.</span></span> <span data-ttu-id="565ed-198">Ancak, veri belirtildiği hello havuzlarını, kopyalanan tooany olabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="565ed-198">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="565ed-199">Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="565ed-199">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="565ed-200">Bağlı hizmet türü [OnPremisesMongoDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="565ed-200">A linked service of type [OnPremisesMongoDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="565ed-201">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="565ed-201">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="565ed-202">Bir giriş [dataset](data-factory-create-datasets.md) türü [MongoDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="565ed-202">An input [dataset](data-factory-create-datasets.md) of type [MongoDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="565ed-203">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="565ed-203">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="565ed-204">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [MongoDbSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="565ed-204">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [MongoDbSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="565ed-205">Merhaba örnek veri MongoDB veritabanı tooa blob bir sorgu sonucunda her saat kopyalar.</span><span class="sxs-lookup"><span data-stu-id="565ed-205">hello sample copies data from a query result in MongoDB database tooa blob every hour.</span></span> <span data-ttu-id="565ed-206">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="565ed-206">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="565ed-207">Merhaba veri yönetimi ağ geçidi hello hello yönergeleri göredir ilk adım olarak, Kurulum [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="565ed-207">As a first step, setup hello data management gateway as per hello instructions in hello [Data Management Gateway](data-factory-data-management-gateway.md) article.</span></span>

<span data-ttu-id="565ed-208">**MongoDB bağlantılı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="565ed-208">**MongoDB linked service:**</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

<span data-ttu-id="565ed-209">**Azure Storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="565ed-209">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="565ed-210">**MongoDB girdi veri kümesi:** "dış" ayarı: "true" bildirir hello Data Factory hizmetinin bu hello tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="565ed-210">**MongoDB input dataset:** Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="565ed-211">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="565ed-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="565ed-212">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="565ed-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="565ed-213">hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="565ed-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="565ed-214">Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="565ed-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="565ed-215">**MongoDB kaynak ve Blob havuz ile ardışık düzeninde etkinlik kopyalayın:**</span><span class="sxs-lookup"><span data-stu-id="565ed-215">**Copy activity in a pipeline with MongoDB source and Blob sink:**</span></span>

<span data-ttu-id="565ed-216">Merhaba ardışık düzen giriş ve çıkış veri kümeleri yukarıda yapılandırılan toouse hello ve zamanlanmış toorun her saatte birdir kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="565ed-216">hello pipeline contains a Copy Activity that is configured toouse hello above input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="565ed-217">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**MongoDbSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="565ed-217">In hello pipeline JSON definition, hello **source** type is set too**MongoDbSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="565ed-218">Merhaba belirtilen hello SQL sorgusu **sorgu** özelliği saat toocopy geçmiş hello hello veri seçer.</span><span class="sxs-lookup"><span data-stu-id="565ed-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
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
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a><span data-ttu-id="565ed-219">Şema tarafından veri fabrikası</span><span class="sxs-lookup"><span data-stu-id="565ed-219">Schema by Data Factory</span></span>
<span data-ttu-id="565ed-220">Azure Data Factory hizmeti hello koleksiyonunda hello son 100 belgeleri kullanarak MongoDB koleksiyonundan şema oluşturur.</span><span class="sxs-lookup"><span data-stu-id="565ed-220">Azure Data Factory service infers schema from a MongoDB collection by using hello latest 100 documents in hello collection.</span></span> <span data-ttu-id="565ed-221">Bu 100 belgeleri tam şema içermiyorsa, bazı sütunları hello kopyalama işlemi sırasında yoksayılabilir.</span><span class="sxs-lookup"><span data-stu-id="565ed-221">If these 100 documents do not contain full schema, some columns may be ignored during hello copy operation.</span></span>

## <a name="type-mapping-for-mongodb"></a><span data-ttu-id="565ed-222">MongoDB için tür eşlemesi</span><span class="sxs-lookup"><span data-stu-id="565ed-222">Type mapping for MongoDB</span></span>
<span data-ttu-id="565ed-223">Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri 2 adımlı yaklaşımı izleyerek hello ile:</span><span class="sxs-lookup"><span data-stu-id="565ed-223">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="565ed-224">Yerel kaynak türleri too.NET türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="565ed-224">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="565ed-225">.NET türü toonative havuz türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="565ed-225">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="565ed-226">Aşağıdaki veri tooMongoDB hello taşırken eşlemeleri MongoDB türleri too.NET türlerinden kullanılır.</span><span class="sxs-lookup"><span data-stu-id="565ed-226">When moving data tooMongoDB hello following mappings are used from MongoDB types too.NET types.</span></span>

| <span data-ttu-id="565ed-227">MongoDB türü</span><span class="sxs-lookup"><span data-stu-id="565ed-227">MongoDB type</span></span> | <span data-ttu-id="565ed-228">.NET framework türü</span><span class="sxs-lookup"><span data-stu-id="565ed-228">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="565ed-229">İkili</span><span class="sxs-lookup"><span data-stu-id="565ed-229">Binary</span></span> |<span data-ttu-id="565ed-230">Byte]</span><span class="sxs-lookup"><span data-stu-id="565ed-230">Byte[]</span></span> |
| <span data-ttu-id="565ed-231">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="565ed-231">Boolean</span></span> |<span data-ttu-id="565ed-232">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="565ed-232">Boolean</span></span> |
| <span data-ttu-id="565ed-233">Tarih</span><span class="sxs-lookup"><span data-stu-id="565ed-233">Date</span></span> |<span data-ttu-id="565ed-234">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="565ed-234">DateTime</span></span> |
| <span data-ttu-id="565ed-235">NumberDouble</span><span class="sxs-lookup"><span data-stu-id="565ed-235">NumberDouble</span></span> |<span data-ttu-id="565ed-236">Çift</span><span class="sxs-lookup"><span data-stu-id="565ed-236">Double</span></span> |
| <span data-ttu-id="565ed-237">NumberInt</span><span class="sxs-lookup"><span data-stu-id="565ed-237">NumberInt</span></span> |<span data-ttu-id="565ed-238">Int32</span><span class="sxs-lookup"><span data-stu-id="565ed-238">Int32</span></span> |
| <span data-ttu-id="565ed-239">NumberLong</span><span class="sxs-lookup"><span data-stu-id="565ed-239">NumberLong</span></span> |<span data-ttu-id="565ed-240">Int64</span><span class="sxs-lookup"><span data-stu-id="565ed-240">Int64</span></span> |
| <span data-ttu-id="565ed-241">ObjectID</span><span class="sxs-lookup"><span data-stu-id="565ed-241">ObjectID</span></span> |<span data-ttu-id="565ed-242">Dize</span><span class="sxs-lookup"><span data-stu-id="565ed-242">String</span></span> |
| <span data-ttu-id="565ed-243">Dize</span><span class="sxs-lookup"><span data-stu-id="565ed-243">String</span></span> |<span data-ttu-id="565ed-244">Dize</span><span class="sxs-lookup"><span data-stu-id="565ed-244">String</span></span> |
| <span data-ttu-id="565ed-245">UUID</span><span class="sxs-lookup"><span data-stu-id="565ed-245">UUID</span></span> |<span data-ttu-id="565ed-246">GUID</span><span class="sxs-lookup"><span data-stu-id="565ed-246">Guid</span></span> |
| <span data-ttu-id="565ed-247">Nesne</span><span class="sxs-lookup"><span data-stu-id="565ed-247">Object</span></span> |<span data-ttu-id="565ed-248">Renormalized içine iç içe geçmiş ayırıcı olarak "_" sütunlarla düzleştirme</span><span class="sxs-lookup"><span data-stu-id="565ed-248">Renormalized into flatten columns with “_” as nested separator</span></span> |

> [!NOTE]
> <span data-ttu-id="565ed-249">Sanal tablolar kullanarak dizileri desteği hakkında toolearn başvurmak çok[sanal tablolar kullanarak karmaşık türleri için destek](#support-for-complex-types-using-virtual-tables) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="565ed-249">toolearn about support for arrays using virtual tables, refer too[Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section below.</span></span>

<span data-ttu-id="565ed-250">Şu anda, şu MongoDB veri türlerini hello desteklenmiyor: DBPointer, JavaScript, en fazla/dak anahtar, normal ifade, simge, zaman damgası, tanımlanmamış</span><span class="sxs-lookup"><span data-stu-id="565ed-250">Currently, hello following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined</span></span>

## <a name="support-for-complex-types-using-virtual-tables"></a><span data-ttu-id="565ed-251">Sanal tablolar kullanarak karmaşık türleri için destek</span><span class="sxs-lookup"><span data-stu-id="565ed-251">Support for complex types using virtual tables</span></span>
<span data-ttu-id="565ed-252">Azure Data Factory bir yerleşik ODBC sürücüsü tooconnect tooand kopyalama veritabanınızdaki verileri MongoDB kullanır.</span><span class="sxs-lookup"><span data-stu-id="565ed-252">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your MongoDB database.</span></span> <span data-ttu-id="565ed-253">Merhaba belgeler arasında farklı türleriyle dizileri veya nesneleri gibi karmaşık türler için hello sürücü veri karşılık gelen sanal tablolara yeniden normalleştirir.</span><span class="sxs-lookup"><span data-stu-id="565ed-253">For complex types such as arrays or objects with different types across hello documents, hello driver re-normalizes data into corresponding virtual tables.</span></span> <span data-ttu-id="565ed-254">Özellikle, bir tablo bu tür sütunlar içeriyorsa, hello sürücü sanal tablolar aşağıdaki hello oluşturur:</span><span class="sxs-lookup"><span data-stu-id="565ed-254">Specifically, if a table contains such columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="565ed-255">A **temel tablo**, içeren hello hello gerçek tablo hello karmaşık tür sütunları dışında aynı verileri.</span><span class="sxs-lookup"><span data-stu-id="565ed-255">A **base table**, which contains hello same data as hello real table except for hello complex type columns.</span></span> <span data-ttu-id="565ed-256">Merhaba temel tablo aynı adı hello temsil ettiği hello gerçek tablo olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="565ed-256">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="565ed-257">A **sanal tablo** her karmaşık tür sütun için hangi genişletir hello iç içe geçmiş verileri.</span><span class="sxs-lookup"><span data-stu-id="565ed-257">A **virtual table** for each complex type column, which expands hello nested data.</span></span> <span data-ttu-id="565ed-258">Merhaba sanal tablolar hello gerçek tablonun hello adı, bir ayırıcı "_" ve hello hello dizi veya nesne adını kullanarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="565ed-258">hello virtual tables are named using hello name of hello real table, a separator “_” and hello name of hello array or object.</span></span>

<span data-ttu-id="565ed-259">Sanal tablolar hello gerçek tablosunda toohello veri bakın, etkinleştirme hello sürücü tooaccess Normalleştirilmemiş veri hello.</span><span class="sxs-lookup"><span data-stu-id="565ed-259">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="565ed-260">Ayrıntılar aşağıda örnek bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="565ed-260">See Example section below details.</span></span> <span data-ttu-id="565ed-261">Sorgulamak ve hello sanal tabloları birleştirme MongoDB dizi hello içeriğe erişebilir.</span><span class="sxs-lookup"><span data-stu-id="565ed-261">You can access hello content of MongoDB arrays by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="565ed-262">Merhaba kullanabilirsiniz [Kopyalama Sihirbazı'nı](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively görünümü hello hello sanal tablolar dahil olmak üzere MongoDB veritabanı tablolarında listesi ve önizleme içindeki hello verileri.</span><span class="sxs-lookup"><span data-stu-id="565ed-262">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in MongoDB database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="565ed-263">Ayrıca, hello Kopyalama Sihirbazı, bir sorgu oluşturun ve toosee hello sonucu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="565ed-263">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="565ed-264">Örnek</span><span class="sxs-lookup"><span data-stu-id="565ed-264">Example</span></span>
<span data-ttu-id="565ed-265">Örneğin, aşağıda "ExampleTable" her hücresinde – faturaları ve bir dizi skaler türler – derecelendirmeleri bir sütunla nesnelerinin bir dizisi ile bir sütunu bulunan bir MongoDB tablodur.</span><span class="sxs-lookup"><span data-stu-id="565ed-265">For example, “ExampleTable” below is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span></span>

| <span data-ttu-id="565ed-266">_ıd</span><span class="sxs-lookup"><span data-stu-id="565ed-266">_id</span></span> | <span data-ttu-id="565ed-267">Müşteri adı</span><span class="sxs-lookup"><span data-stu-id="565ed-267">Customer Name</span></span> | <span data-ttu-id="565ed-268">Faturalar</span><span class="sxs-lookup"><span data-stu-id="565ed-268">Invoices</span></span> | <span data-ttu-id="565ed-269">Hizmet düzeyi</span><span class="sxs-lookup"><span data-stu-id="565ed-269">Service Level</span></span> | <span data-ttu-id="565ed-270">Derecelendirme</span><span class="sxs-lookup"><span data-stu-id="565ed-270">Ratings</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="565ed-271">1111</span><span class="sxs-lookup"><span data-stu-id="565ed-271">1111</span></span> |<span data-ttu-id="565ed-272">ABC</span><span class="sxs-lookup"><span data-stu-id="565ed-272">ABC</span></span> |<span data-ttu-id="565ed-273">[{invoice_id: "123" öğesi: "toaster", fiyat: "456", indirim: "0.2"}, {invoice_id: "124" öğesi: "fırın", fiyat: "1235" indirim: "0.2"}]</span><span class="sxs-lookup"><span data-stu-id="565ed-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span></span> |<span data-ttu-id="565ed-274">Gümüş</span><span class="sxs-lookup"><span data-stu-id="565ed-274">Silver</span></span> |<span data-ttu-id="565ed-275">[5,6]</span><span class="sxs-lookup"><span data-stu-id="565ed-275">[5,6]</span></span> |
| <span data-ttu-id="565ed-276">2222</span><span class="sxs-lookup"><span data-stu-id="565ed-276">2222</span></span> |<span data-ttu-id="565ed-277">XYZ</span><span class="sxs-lookup"><span data-stu-id="565ed-277">XYZ</span></span> |<span data-ttu-id="565ed-278">[{invoice_id: "135" öğesi: "fridge", fiyat: "12543", indirim: "0,0"}]</span><span class="sxs-lookup"><span data-stu-id="565ed-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span></span> |<span data-ttu-id="565ed-279">Altın</span><span class="sxs-lookup"><span data-stu-id="565ed-279">Gold</span></span> |<span data-ttu-id="565ed-280">[1,2]</span><span class="sxs-lookup"><span data-stu-id="565ed-280">[1,2]</span></span> |

<span data-ttu-id="565ed-281">Merhaba sürücüsü birden çok sanal tablolar toorepresent bu tek tablo oluşturur.</span><span class="sxs-lookup"><span data-stu-id="565ed-281">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="565ed-282">Merhaba ilk sanal hello temel tablo "aşağıda gösterilen ExampleTable" adlı bir tablodur.</span><span class="sxs-lookup"><span data-stu-id="565ed-282">hello first virtual table is hello base table named “ExampleTable”, shown below.</span></span> <span data-ttu-id="565ed-283">Hello temel tablo hello orijinal tablonun tüm hello verileri içerir, ancak hello diziler hello verilerden çıkarıldı ve hello sanal tablolarda genişletilir.</span><span class="sxs-lookup"><span data-stu-id="565ed-283">hello base table contains all hello data of hello original table, but hello data from hello arrays has been omitted and is expanded in hello virtual tables.</span></span>

| <span data-ttu-id="565ed-284">_ıd</span><span class="sxs-lookup"><span data-stu-id="565ed-284">_id</span></span> | <span data-ttu-id="565ed-285">Müşteri adı</span><span class="sxs-lookup"><span data-stu-id="565ed-285">Customer Name</span></span> | <span data-ttu-id="565ed-286">Hizmet düzeyi</span><span class="sxs-lookup"><span data-stu-id="565ed-286">Service Level</span></span> |
| --- | --- | --- |
| <span data-ttu-id="565ed-287">1111</span><span class="sxs-lookup"><span data-stu-id="565ed-287">1111</span></span> |<span data-ttu-id="565ed-288">ABC</span><span class="sxs-lookup"><span data-stu-id="565ed-288">ABC</span></span> |<span data-ttu-id="565ed-289">Gümüş</span><span class="sxs-lookup"><span data-stu-id="565ed-289">Silver</span></span> |
| <span data-ttu-id="565ed-290">2222</span><span class="sxs-lookup"><span data-stu-id="565ed-290">2222</span></span> |<span data-ttu-id="565ed-291">XYZ</span><span class="sxs-lookup"><span data-stu-id="565ed-291">XYZ</span></span> |<span data-ttu-id="565ed-292">Altın</span><span class="sxs-lookup"><span data-stu-id="565ed-292">Gold</span></span> |

<span data-ttu-id="565ed-293">Merhaba aşağıdaki tablolarda hello hello özgün diziler hello örnekte temsil eden sanal tablolar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="565ed-293">hello following tables show hello virtual tables that represent hello original arrays in hello example.</span></span> <span data-ttu-id="565ed-294">Bu tablolar hello aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="565ed-294">These tables contain hello following:</span></span>

* <span data-ttu-id="565ed-295">Bir başvuru geri toohello özgün birincil anahtar sütunu karşılık gelen toohello satır hello özgün dizinin (aracılığıyla hello _ıd sütun)</span><span class="sxs-lookup"><span data-stu-id="565ed-295">A reference back toohello original primary key column corresponding toohello row of hello original array (via hello _id column)</span></span>
* <span data-ttu-id="565ed-296">Merhaba konumunu hello özgün dizi hello verilerini bir göstergesi</span><span class="sxs-lookup"><span data-stu-id="565ed-296">An indication of hello position of hello data within hello original array</span></span>
* <span data-ttu-id="565ed-297">Merhaba veri hello dizi her öğe için genişletilmiş</span><span class="sxs-lookup"><span data-stu-id="565ed-297">hello expanded data for each element within hello array</span></span>

<span data-ttu-id="565ed-298">Tablo "ExampleTable_Invoices":</span><span class="sxs-lookup"><span data-stu-id="565ed-298">Table “ExampleTable_Invoices”:</span></span>

| <span data-ttu-id="565ed-299">_ıd</span><span class="sxs-lookup"><span data-stu-id="565ed-299">_id</span></span> | <span data-ttu-id="565ed-300">ExampleTable_Invoices_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="565ed-300">ExampleTable_Invoices_dim1_idx</span></span> | <span data-ttu-id="565ed-301">invoice_id</span><span class="sxs-lookup"><span data-stu-id="565ed-301">invoice_id</span></span> | <span data-ttu-id="565ed-302">Öğesi</span><span class="sxs-lookup"><span data-stu-id="565ed-302">item</span></span> | <span data-ttu-id="565ed-303">price</span><span class="sxs-lookup"><span data-stu-id="565ed-303">price</span></span> | <span data-ttu-id="565ed-304">İndirim</span><span class="sxs-lookup"><span data-stu-id="565ed-304">Discount</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="565ed-305">1111</span><span class="sxs-lookup"><span data-stu-id="565ed-305">1111</span></span> |<span data-ttu-id="565ed-306">0</span><span class="sxs-lookup"><span data-stu-id="565ed-306">0</span></span> |<span data-ttu-id="565ed-307">123</span><span class="sxs-lookup"><span data-stu-id="565ed-307">123</span></span> |<span data-ttu-id="565ed-308">toaster</span><span class="sxs-lookup"><span data-stu-id="565ed-308">toaster</span></span> |<span data-ttu-id="565ed-309">456</span><span class="sxs-lookup"><span data-stu-id="565ed-309">456</span></span> |<span data-ttu-id="565ed-310">0.2</span><span class="sxs-lookup"><span data-stu-id="565ed-310">0.2</span></span> |
| <span data-ttu-id="565ed-311">1111</span><span class="sxs-lookup"><span data-stu-id="565ed-311">1111</span></span> |<span data-ttu-id="565ed-312">1</span><span class="sxs-lookup"><span data-stu-id="565ed-312">1</span></span> |<span data-ttu-id="565ed-313">124</span><span class="sxs-lookup"><span data-stu-id="565ed-313">124</span></span> |<span data-ttu-id="565ed-314">Fırın</span><span class="sxs-lookup"><span data-stu-id="565ed-314">oven</span></span> |<span data-ttu-id="565ed-315">1235</span><span class="sxs-lookup"><span data-stu-id="565ed-315">1235</span></span> |<span data-ttu-id="565ed-316">0.2</span><span class="sxs-lookup"><span data-stu-id="565ed-316">0.2</span></span> |
| <span data-ttu-id="565ed-317">2222</span><span class="sxs-lookup"><span data-stu-id="565ed-317">2222</span></span> |<span data-ttu-id="565ed-318">0</span><span class="sxs-lookup"><span data-stu-id="565ed-318">0</span></span> |<span data-ttu-id="565ed-319">135</span><span class="sxs-lookup"><span data-stu-id="565ed-319">135</span></span> |<span data-ttu-id="565ed-320">fridge</span><span class="sxs-lookup"><span data-stu-id="565ed-320">fridge</span></span> |<span data-ttu-id="565ed-321">12543</span><span class="sxs-lookup"><span data-stu-id="565ed-321">12543</span></span> |<span data-ttu-id="565ed-322">0.0</span><span class="sxs-lookup"><span data-stu-id="565ed-322">0.0</span></span> |

<span data-ttu-id="565ed-323">Tablo "ExampleTable_Ratings":</span><span class="sxs-lookup"><span data-stu-id="565ed-323">Table “ExampleTable_Ratings”:</span></span>

| <span data-ttu-id="565ed-324">_ıd</span><span class="sxs-lookup"><span data-stu-id="565ed-324">_id</span></span> | <span data-ttu-id="565ed-325">ExampleTable_Ratings_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="565ed-325">ExampleTable_Ratings_dim1_idx</span></span> | <span data-ttu-id="565ed-326">ExampleTable_Ratings</span><span class="sxs-lookup"><span data-stu-id="565ed-326">ExampleTable_Ratings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="565ed-327">1111</span><span class="sxs-lookup"><span data-stu-id="565ed-327">1111</span></span> |<span data-ttu-id="565ed-328">0</span><span class="sxs-lookup"><span data-stu-id="565ed-328">0</span></span> |<span data-ttu-id="565ed-329">5</span><span class="sxs-lookup"><span data-stu-id="565ed-329">5</span></span> |
| <span data-ttu-id="565ed-330">1111</span><span class="sxs-lookup"><span data-stu-id="565ed-330">1111</span></span> |<span data-ttu-id="565ed-331">1</span><span class="sxs-lookup"><span data-stu-id="565ed-331">1</span></span> |<span data-ttu-id="565ed-332">6</span><span class="sxs-lookup"><span data-stu-id="565ed-332">6</span></span> |
| <span data-ttu-id="565ed-333">2222</span><span class="sxs-lookup"><span data-stu-id="565ed-333">2222</span></span> |<span data-ttu-id="565ed-334">0</span><span class="sxs-lookup"><span data-stu-id="565ed-334">0</span></span> |<span data-ttu-id="565ed-335">1</span><span class="sxs-lookup"><span data-stu-id="565ed-335">1</span></span> |
| <span data-ttu-id="565ed-336">2222</span><span class="sxs-lookup"><span data-stu-id="565ed-336">2222</span></span> |<span data-ttu-id="565ed-337">1</span><span class="sxs-lookup"><span data-stu-id="565ed-337">1</span></span> |<span data-ttu-id="565ed-338">2</span><span class="sxs-lookup"><span data-stu-id="565ed-338">2</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="565ed-339">Kaynak toosink sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="565ed-339">Map source toosink columns</span></span>
<span data-ttu-id="565ed-340">Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="565ed-340">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="565ed-341">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="565ed-341">Repeatable read from relational sources</span></span>
<span data-ttu-id="565ed-342">İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları.</span><span class="sxs-lookup"><span data-stu-id="565ed-342">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="565ed-343">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="565ed-343">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="565ed-344">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="565ed-344">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="565ed-345">Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="565ed-345">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="565ed-346">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="565ed-346">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="565ed-347">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="565ed-347">Performance and Tuning</span></span>
<span data-ttu-id="565ed-348">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="565ed-348">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="565ed-349">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="565ed-349">Next Steps</span></span>
<span data-ttu-id="565ed-350">Bkz: [şirket içi ve bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) veri ardışık oluşturma verileri şirket verilerinden depolamak tooan Azure veri deposu taşır için adım adım yönergeler için makalesi.</span><span class="sxs-lookup"><span data-stu-id="565ed-350">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions for creating a data pipeline that moves data from an on-premises data store tooan Azure data store.</span></span>
