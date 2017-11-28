---
title: Azure Data Factory kullanarak Teradata aaaMove verilerden | Microsoft Docs
description: "Merhaba Teradata veritabanından veri taşımanıza olanak tanır Data Factory hizmeti için Teradata Bağlayıcısı hakkında bilgi edinin"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 98eb76d8-5f3d-4667-b76e-e59ed3eea3ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 79153476157666463b499edaa7585adaf8ad3bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="3154e-103">Azure Data Factory kullanarak Teradata taşıma verileri</span><span class="sxs-lookup"><span data-stu-id="3154e-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="3154e-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri bir şirket içi Teradata veritabanından açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3154e-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Teradata database.</span></span> <span data-ttu-id="3154e-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="3154e-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="3154e-106">Bir şirket içi Teradata veri deposu desteklenen tooany havuz veri deposundan verileri kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3154e-106">You can copy data from an on-premises Teradata data store tooany supported sink data store.</span></span> <span data-ttu-id="3154e-107">Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="3154e-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="3154e-108">Veri Fabrikası şu anda verileri Teradata verilerinden tooother veri depolarına depolamak taşıma yalnızca, ancak diğer veri depoları tooa Teradata veri deposundan veri taşıma değil destekler.</span><span class="sxs-lookup"><span data-stu-id="3154e-108">Data factory currently supports only moving data from a Teradata data store tooother data stores, but not for moving data from other data stores tooa Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3154e-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3154e-109">Prerequisites</span></span>
<span data-ttu-id="3154e-110">Veri Fabrikası hello veri yönetimi ağ geçidi üzerinden bağlanan tooon içi Teradata kaynakları destekler.</span><span class="sxs-lookup"><span data-stu-id="3154e-110">Data factory supports connecting tooon-premises Teradata sources via hello Data Management Gateway.</span></span> <span data-ttu-id="3154e-111">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale toolearn veri yönetimi ağ geçidi ve hello ağ geçidi kurun ayarlama hakkında adım adım yönergeleri hakkında.</span><span class="sxs-lookup"><span data-stu-id="3154e-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="3154e-112">Merhaba Teradata bir Azure Iaas sanal barındırılan olsa bile ağ geçidi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3154e-112">Gateway is required even if hello Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="3154e-113">Merhaba ağ geçidi üzerinde aynı Iaas VM hello veri olarak depolamak veya hello ağ geçidi olarak aynı uzunlukta farklı bir VM üzerinde toohello veritabanı bağlanabilir hello yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3154e-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="3154e-114">Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="3154e-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="3154e-115">Desteklenen sürümleri ve yükleme</span><span class="sxs-lookup"><span data-stu-id="3154e-115">Supported versions and installation</span></span>
<span data-ttu-id="3154e-116">Veri Yönetimi ağ geçidi tooconnect toohello Teradata veritabanına için ihtiyacınız tooinstall hello [Teradata için .NET veri sağlayıcısı](http://go.microsoft.com/fwlink/?LinkId=278886) sürüm 14 veya yukarıdaki üzerinde aynı hello veri yönetimi ağ geçidi hello gibi sistem.</span><span class="sxs-lookup"><span data-stu-id="3154e-116">For Data Management Gateway tooconnect toohello Teradata Database, you need tooinstall hello [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="3154e-117">Teradata sürüm 12 ve üzeri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="3154e-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="3154e-118">Başlarken</span><span class="sxs-lookup"><span data-stu-id="3154e-118">Getting started</span></span>
<span data-ttu-id="3154e-119">Farklı araçlar/API'lerini kullanarak bir şirket içi Cassandra veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3154e-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="3154e-120">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="3154e-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="3154e-121">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="3154e-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="3154e-122">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="3154e-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="3154e-123">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="3154e-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="3154e-124">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3154e-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="3154e-125">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="3154e-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="3154e-126">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="3154e-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="3154e-127">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="3154e-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="3154e-128">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3154e-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="3154e-129">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="3154e-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="3154e-130">Bir şirket içi Teradata veri deposundaki kullanılan toocopy verileri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: Teradata tooAzure Blob veri kopyalama](#json-example-copy-data-from-teradata-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="3154e-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata tooAzure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="3154e-131">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooa Teradata veri deposu olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="3154e-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="3154e-132">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="3154e-132">Linked service properties</span></span>
<span data-ttu-id="3154e-133">Aşağıdaki tablonun hello JSON öğeleri belirli tooTeradata bağlantılı hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="3154e-133">hello following table provides description for JSON elements specific tooTeradata linked service.</span></span>

| <span data-ttu-id="3154e-134">Özellik</span><span class="sxs-lookup"><span data-stu-id="3154e-134">Property</span></span> | <span data-ttu-id="3154e-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3154e-135">Description</span></span> | <span data-ttu-id="3154e-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3154e-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3154e-137">type</span><span class="sxs-lookup"><span data-stu-id="3154e-137">type</span></span> |<span data-ttu-id="3154e-138">Merhaba type özelliği ayarlanmalıdır: **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="3154e-138">hello type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="3154e-139">Evet</span><span class="sxs-lookup"><span data-stu-id="3154e-139">Yes</span></span> |
| <span data-ttu-id="3154e-140">sunucu</span><span class="sxs-lookup"><span data-stu-id="3154e-140">server</span></span> |<span data-ttu-id="3154e-141">Merhaba Teradata sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="3154e-141">Name of hello Teradata server.</span></span> |<span data-ttu-id="3154e-142">Evet</span><span class="sxs-lookup"><span data-stu-id="3154e-142">Yes</span></span> |
| <span data-ttu-id="3154e-143">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3154e-143">authenticationType</span></span> |<span data-ttu-id="3154e-144">Kimlik doğrulama türü tooconnect toohello Teradata veritabanına kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3154e-144">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="3154e-145">Olası değerler şunlardır: Anonim, temel ve Windows.</span><span class="sxs-lookup"><span data-stu-id="3154e-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="3154e-146">Evet</span><span class="sxs-lookup"><span data-stu-id="3154e-146">Yes</span></span> |
| <span data-ttu-id="3154e-147">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="3154e-147">username</span></span> |<span data-ttu-id="3154e-148">Temel veya Windows kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="3154e-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="3154e-149">Hayır</span><span class="sxs-lookup"><span data-stu-id="3154e-149">No</span></span> |
| <span data-ttu-id="3154e-150">password</span><span class="sxs-lookup"><span data-stu-id="3154e-150">password</span></span> |<span data-ttu-id="3154e-151">Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="3154e-151">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="3154e-152">Hayır</span><span class="sxs-lookup"><span data-stu-id="3154e-152">No</span></span> |
| <span data-ttu-id="3154e-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3154e-153">gatewayName</span></span> |<span data-ttu-id="3154e-154">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi Teradata veritabanına kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3154e-154">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="3154e-155">Evet</span><span class="sxs-lookup"><span data-stu-id="3154e-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="3154e-156">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="3154e-156">Dataset properties</span></span>
<span data-ttu-id="3154e-157">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="3154e-157">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="3154e-158">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="3154e-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="3154e-159">Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="3154e-159">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="3154e-160">Şu anda hello Teradata veri kümesi için desteklenen tür özellik yok.</span><span class="sxs-lookup"><span data-stu-id="3154e-160">Currently, there are no type properties supported for hello Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="3154e-161">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="3154e-161">Copy activity properties</span></span>
<span data-ttu-id="3154e-162">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="3154e-162">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="3154e-163">Ad, açıklama, giriş ve çıkış tabloları ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3154e-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="3154e-164">Oysa hello typeProperties bölümünde hello etkinlik özellikleri her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="3154e-164">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="3154e-165">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="3154e-165">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="3154e-166">Merhaba kaynak türü olduğunda **RelationalSource** (içeren Teradata), aşağıdaki özelliklere hello kullanılabilir **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="3154e-166">When hello source is of type **RelationalSource** (which includes Teradata), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="3154e-167">Özellik</span><span class="sxs-lookup"><span data-stu-id="3154e-167">Property</span></span> | <span data-ttu-id="3154e-168">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3154e-168">Description</span></span> | <span data-ttu-id="3154e-169">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="3154e-169">Allowed values</span></span> | <span data-ttu-id="3154e-170">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3154e-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3154e-171">sorgu</span><span class="sxs-lookup"><span data-stu-id="3154e-171">query</span></span> |<span data-ttu-id="3154e-172">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="3154e-172">Use hello custom query tooread data.</span></span> |<span data-ttu-id="3154e-173">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="3154e-173">SQL query string.</span></span> <span data-ttu-id="3154e-174">Örneğin: seçin * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="3154e-174">For example: select * from MyTable.</span></span> |<span data-ttu-id="3154e-175">Evet</span><span class="sxs-lookup"><span data-stu-id="3154e-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-tooazure-blob"></a><span data-ttu-id="3154e-176">JSON örnek: Teradata tooAzure Blob veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="3154e-176">JSON example: Copy data from Teradata tooAzure Blob</span></span>
<span data-ttu-id="3154e-177">Merhaba aşağıdaki örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3154e-177">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="3154e-178">Bunlar Göster nasıl Teradata tooAzure Blob Storage toocopy verileri.</span><span class="sxs-lookup"><span data-stu-id="3154e-178">They show how toocopy data from Teradata tooAzure Blob Storage.</span></span> <span data-ttu-id="3154e-179">Ancak, veri belirtildiği hello havuzlarını, kopyalanan tooany olabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="3154e-179">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="3154e-180">Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="3154e-180">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="3154e-181">Bağlı hizmet türü [OnPremisesTeradata](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3154e-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="3154e-182">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3154e-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="3154e-183">Bir giriş [dataset](data-factory-create-datasets.md) türü [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3154e-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="3154e-184">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3154e-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="3154e-185">Merhaba [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="3154e-185">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="3154e-186">Merhaba örnek veri Teradata veritabanına tooa blob bir sorgu sonucunda her saat kopyalar.</span><span class="sxs-lookup"><span data-stu-id="3154e-186">hello sample copies data from a query result in Teradata database tooa blob every hour.</span></span> <span data-ttu-id="3154e-187">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="3154e-187">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="3154e-188">İlk adım olarak, hello veri yönetimi ağ geçidi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3154e-188">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="3154e-189">Merhaba yönergelerdir hello [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="3154e-189">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="3154e-190">**Teradata bağlantılı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="3154e-190">**Teradata linked service:**</span></span>

```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="3154e-191">**Azure Blob storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="3154e-191">**Azure Blob storage linked service:**</span></span>

```json
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

<span data-ttu-id="3154e-192">**Teradata girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="3154e-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="3154e-193">Merhaba örnek bir tablo "MyTable" Teradata içinde oluşturduğunuz ve zaman serisi veri için "zaman damgası" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="3154e-193">hello sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="3154e-194">"Dış" ayarı: true, o hello tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil hello Data Factory hizmetinin bildirir.</span><span class="sxs-lookup"><span data-stu-id="3154e-194">Setting “external”: true informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "TeradataDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {
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

<span data-ttu-id="3154e-195">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="3154e-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="3154e-196">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="3154e-196">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="3154e-197">hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="3154e-197">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="3154e-198">Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="3154e-198">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobTeradataDataSet",
    "properties": {
        "published": false,
        "location": {
            "type": "AzureBlobLocation",
            "folderPath": "mycontainer/teradata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            ],
            "linkedServiceName": "AzureStorageLinkedService"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="3154e-199">**Kopyalama etkinliği ile kanal:**</span><span class="sxs-lookup"><span data-stu-id="3154e-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="3154e-200">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun saatlik ise.</span><span class="sxs-lookup"><span data-stu-id="3154e-200">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="3154e-201">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**RelationalSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="3154e-201">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="3154e-202">Merhaba belirtilen hello SQL sorgusu **sorgu** özelliği saat toocopy geçmiş hello hello veri seçer.</span><span class="sxs-lookup"><span data-stu-id="3154e-202">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "TeradataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobTeradataDataSet"
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
                "name": "TeradataToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z",
        "isPaused": false
    }
}
```
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="3154e-203">Teradata için tür eşlemesi</span><span class="sxs-lookup"><span data-stu-id="3154e-203">Type mapping for Teradata</span></span>
<span data-ttu-id="3154e-204">Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, hello kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri 2 adımlı yaklaşımı izleyerek hello ile:</span><span class="sxs-lookup"><span data-stu-id="3154e-204">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="3154e-205">Yerel kaynak türleri too.NET türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="3154e-205">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="3154e-206">.NET türü toonative havuz türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="3154e-206">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="3154e-207">Veri tooTeradata taşırken hello aşağıdaki eşlemelerini Teradata türü too.NET türünden kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3154e-207">When moving data tooTeradata, hello following mappings are used from Teradata type too.NET type.</span></span>

| <span data-ttu-id="3154e-208">Teradata veritabanına türü</span><span class="sxs-lookup"><span data-stu-id="3154e-208">Teradata Database type</span></span> | <span data-ttu-id="3154e-209">.NET framework türü</span><span class="sxs-lookup"><span data-stu-id="3154e-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="3154e-210">char</span><span class="sxs-lookup"><span data-stu-id="3154e-210">Char</span></span> |<span data-ttu-id="3154e-211">Dize</span><span class="sxs-lookup"><span data-stu-id="3154e-211">String</span></span> |
| <span data-ttu-id="3154e-212">CLOB</span><span class="sxs-lookup"><span data-stu-id="3154e-212">Clob</span></span> |<span data-ttu-id="3154e-213">Dize</span><span class="sxs-lookup"><span data-stu-id="3154e-213">String</span></span> |
| <span data-ttu-id="3154e-214">Grafiği</span><span class="sxs-lookup"><span data-stu-id="3154e-214">Graphic</span></span> |<span data-ttu-id="3154e-215">Dize</span><span class="sxs-lookup"><span data-stu-id="3154e-215">String</span></span> |
| <span data-ttu-id="3154e-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="3154e-216">VarChar</span></span> |<span data-ttu-id="3154e-217">Dize</span><span class="sxs-lookup"><span data-stu-id="3154e-217">String</span></span> |
| <span data-ttu-id="3154e-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="3154e-218">VarGraphic</span></span> |<span data-ttu-id="3154e-219">Dize</span><span class="sxs-lookup"><span data-stu-id="3154e-219">String</span></span> |
| <span data-ttu-id="3154e-220">Blob</span><span class="sxs-lookup"><span data-stu-id="3154e-220">Blob</span></span> |<span data-ttu-id="3154e-221">Byte]</span><span class="sxs-lookup"><span data-stu-id="3154e-221">Byte[]</span></span> |
| <span data-ttu-id="3154e-222">Bayt</span><span class="sxs-lookup"><span data-stu-id="3154e-222">Byte</span></span> |<span data-ttu-id="3154e-223">Byte]</span><span class="sxs-lookup"><span data-stu-id="3154e-223">Byte[]</span></span> |
| <span data-ttu-id="3154e-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="3154e-224">VarByte</span></span> |<span data-ttu-id="3154e-225">Byte]</span><span class="sxs-lookup"><span data-stu-id="3154e-225">Byte[]</span></span> |
| <span data-ttu-id="3154e-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="3154e-226">BigInt</span></span> |<span data-ttu-id="3154e-227">Int64</span><span class="sxs-lookup"><span data-stu-id="3154e-227">Int64</span></span> |
| <span data-ttu-id="3154e-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="3154e-228">ByteInt</span></span> |<span data-ttu-id="3154e-229">Int16</span><span class="sxs-lookup"><span data-stu-id="3154e-229">Int16</span></span> |
| <span data-ttu-id="3154e-230">Ondalık</span><span class="sxs-lookup"><span data-stu-id="3154e-230">Decimal</span></span> |<span data-ttu-id="3154e-231">Ondalık</span><span class="sxs-lookup"><span data-stu-id="3154e-231">Decimal</span></span> |
| <span data-ttu-id="3154e-232">Çift</span><span class="sxs-lookup"><span data-stu-id="3154e-232">Double</span></span> |<span data-ttu-id="3154e-233">Çift</span><span class="sxs-lookup"><span data-stu-id="3154e-233">Double</span></span> |
| <span data-ttu-id="3154e-234">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="3154e-234">Integer</span></span> |<span data-ttu-id="3154e-235">Int32</span><span class="sxs-lookup"><span data-stu-id="3154e-235">Int32</span></span> |
| <span data-ttu-id="3154e-236">Sayı</span><span class="sxs-lookup"><span data-stu-id="3154e-236">Number</span></span> |<span data-ttu-id="3154e-237">Çift</span><span class="sxs-lookup"><span data-stu-id="3154e-237">Double</span></span> |
| <span data-ttu-id="3154e-238">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="3154e-238">SmallInt</span></span> |<span data-ttu-id="3154e-239">Int16</span><span class="sxs-lookup"><span data-stu-id="3154e-239">Int16</span></span> |
| <span data-ttu-id="3154e-240">Tarih</span><span class="sxs-lookup"><span data-stu-id="3154e-240">Date</span></span> |<span data-ttu-id="3154e-241">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="3154e-241">DateTime</span></span> |
| <span data-ttu-id="3154e-242">Zaman</span><span class="sxs-lookup"><span data-stu-id="3154e-242">Time</span></span> |<span data-ttu-id="3154e-243">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3154e-243">TimeSpan</span></span> |
| <span data-ttu-id="3154e-244">Saat dilimi süresiyle</span><span class="sxs-lookup"><span data-stu-id="3154e-244">Time With Time Zone</span></span> |<span data-ttu-id="3154e-245">Dize</span><span class="sxs-lookup"><span data-stu-id="3154e-245">String</span></span> |
| <span data-ttu-id="3154e-246">zaman damgası</span><span class="sxs-lookup"><span data-stu-id="3154e-246">Timestamp</span></span> |<span data-ttu-id="3154e-247">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="3154e-247">DateTime</span></span> |
| <span data-ttu-id="3154e-248">Saat dilimi zaman damgası</span><span class="sxs-lookup"><span data-stu-id="3154e-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="3154e-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="3154e-249">DateTimeOffset</span></span> |
| <span data-ttu-id="3154e-250">Aralık gün</span><span class="sxs-lookup"><span data-stu-id="3154e-250">Interval Day</span></span> |<span data-ttu-id="3154e-251">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3154e-251">TimeSpan</span></span> |
| <span data-ttu-id="3154e-252">Aralık gün tooHour</span><span class="sxs-lookup"><span data-stu-id="3154e-252">Interval Day tooHour</span></span> |<span data-ttu-id="3154e-253">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3154e-253">TimeSpan</span></span> |
| <span data-ttu-id="3154e-254">Aralık gün tooMinute</span><span class="sxs-lookup"><span data-stu-id="3154e-254">Interval Day tooMinute</span></span> |<span data-ttu-id="3154e-255">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3154e-255">TimeSpan</span></span> |
| <span data-ttu-id="3154e-256">Aralık gün tooSecond</span><span class="sxs-lookup"><span data-stu-id="3154e-256">Interval Day tooSecond</span></span> |<span data-ttu-id="3154e-257">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3154e-257">TimeSpan</span></span> |
| <span data-ttu-id="3154e-258">Aralık saat</span><span class="sxs-lookup"><span data-stu-id="3154e-258">Interval Hour</span></span> |<span data-ttu-id="3154e-259">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3154e-259">TimeSpan</span></span> |
| <span data-ttu-id="3154e-260">Aralık saat tooMinute</span><span class="sxs-lookup"><span data-stu-id="3154e-260">Interval Hour tooMinute</span></span> |<span data-ttu-id="3154e-261">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3154e-261">TimeSpan</span></span> |
| <span data-ttu-id="3154e-262">Aralık saat tooSecond</span><span class="sxs-lookup"><span data-stu-id="3154e-262">Interval Hour tooSecond</span></span> |<span data-ttu-id="3154e-263">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3154e-263">TimeSpan</span></span> |
| <span data-ttu-id="3154e-264">Aralık dakika</span><span class="sxs-lookup"><span data-stu-id="3154e-264">Interval Minute</span></span> |<span data-ttu-id="3154e-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3154e-265">TimeSpan</span></span> |
| <span data-ttu-id="3154e-266">Aralık dakika tooSecond</span><span class="sxs-lookup"><span data-stu-id="3154e-266">Interval Minute tooSecond</span></span> |<span data-ttu-id="3154e-267">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3154e-267">TimeSpan</span></span> |
| <span data-ttu-id="3154e-268">Aralığı ikinci</span><span class="sxs-lookup"><span data-stu-id="3154e-268">Interval Second</span></span> |<span data-ttu-id="3154e-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3154e-269">TimeSpan</span></span> |
| <span data-ttu-id="3154e-270">Aralığı yıl</span><span class="sxs-lookup"><span data-stu-id="3154e-270">Interval Year</span></span> |<span data-ttu-id="3154e-271">Dize</span><span class="sxs-lookup"><span data-stu-id="3154e-271">String</span></span> |
| <span data-ttu-id="3154e-272">Aralığı yıl tooMonth</span><span class="sxs-lookup"><span data-stu-id="3154e-272">Interval Year tooMonth</span></span> |<span data-ttu-id="3154e-273">Dize</span><span class="sxs-lookup"><span data-stu-id="3154e-273">String</span></span> |
| <span data-ttu-id="3154e-274">Aralık ayı</span><span class="sxs-lookup"><span data-stu-id="3154e-274">Interval Month</span></span> |<span data-ttu-id="3154e-275">Dize</span><span class="sxs-lookup"><span data-stu-id="3154e-275">String</span></span> |
| <span data-ttu-id="3154e-276">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="3154e-276">Period(Date)</span></span> |<span data-ttu-id="3154e-277">Dize</span><span class="sxs-lookup"><span data-stu-id="3154e-277">String</span></span> |
| <span data-ttu-id="3154e-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="3154e-278">Period(Time)</span></span> |<span data-ttu-id="3154e-279">Dize</span><span class="sxs-lookup"><span data-stu-id="3154e-279">String</span></span> |
| <span data-ttu-id="3154e-280">Süresi (saat dilimi ile)</span><span class="sxs-lookup"><span data-stu-id="3154e-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="3154e-281">Dize</span><span class="sxs-lookup"><span data-stu-id="3154e-281">String</span></span> |
| <span data-ttu-id="3154e-282">Period(timestamp)</span><span class="sxs-lookup"><span data-stu-id="3154e-282">Period(Timestamp)</span></span> |<span data-ttu-id="3154e-283">Dize</span><span class="sxs-lookup"><span data-stu-id="3154e-283">String</span></span> |
| <span data-ttu-id="3154e-284">Süre (saat dilimi damgasıyla)</span><span class="sxs-lookup"><span data-stu-id="3154e-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="3154e-285">Dize</span><span class="sxs-lookup"><span data-stu-id="3154e-285">String</span></span> |
| <span data-ttu-id="3154e-286">XML</span><span class="sxs-lookup"><span data-stu-id="3154e-286">Xml</span></span> |<span data-ttu-id="3154e-287">Dize</span><span class="sxs-lookup"><span data-stu-id="3154e-287">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="3154e-288">Kaynak toosink sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="3154e-288">Map source toosink columns</span></span>
<span data-ttu-id="3154e-289">Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="3154e-289">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="3154e-290">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="3154e-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="3154e-291">İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları.</span><span class="sxs-lookup"><span data-stu-id="3154e-291">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="3154e-292">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3154e-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="3154e-293">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3154e-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="3154e-294">Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3154e-294">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="3154e-295">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="3154e-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="3154e-296">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="3154e-296">Performance and Tuning</span></span>
<span data-ttu-id="3154e-297">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="3154e-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
