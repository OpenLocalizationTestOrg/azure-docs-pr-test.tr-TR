---
title: Azure Data Factory kullanarak SAP Business Warehouse aaaMove verilerden | Microsoft Docs
description: "Hakkında bilgi edinin Azure Data Factory kullanarak SAP Business Warehouse toomove verileri."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 85df16f4759a846f578cad301e3cf918179143d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="ebfd5-103">Veri alanından SAP Business Azure Data Factory kullanarak ambar taşıma</span><span class="sxs-lookup"><span data-stu-id="ebfd5-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="ebfd5-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri bir şirket içi SAP Business Warehouse (BW) gelen açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="ebfd5-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="ebfd5-106">Bir şirket içi SAP Business Warehouse veri deposu desteklenen tooany havuz veri deposundan verileri kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-106">You can copy data from an on-premises SAP Business Warehouse data store tooany supported sink data store.</span></span> <span data-ttu-id="ebfd5-107">Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="ebfd5-108">Veri Fabrikası şu anda destekleyen bir SAP Business Warehouse tooother verilerden veri depolar, ancak taşıma yalnızca verileri diğer veriler taşıma tooan SAP Business Warehouse depolar için.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-108">Data factory currently supports only moving data from an SAP Business Warehouse tooother data stores, but not for moving data from other data stores tooan SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="ebfd5-109">Desteklenen sürümleri ve yükleme</span><span class="sxs-lookup"><span data-stu-id="ebfd5-109">Supported versions and installation</span></span>
<span data-ttu-id="ebfd5-110">Bu bağlayıcı SAP Business Warehouse sürümünü destekleyen 7.x.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="ebfd5-111">MDX sorguları kullanarak veri kopyalamayı Infocubes ve QueryCubes (dahil olmak üzere BEx sorgular) destekler.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="ebfd5-112">tooenable hello bağlantı toohello SAP BW örneği bileşenleri aşağıdaki hello yükleyin:</span><span class="sxs-lookup"><span data-stu-id="ebfd5-112">tooenable hello connectivity toohello SAP BW instance, install hello following components:</span></span>
- <span data-ttu-id="ebfd5-113">**Veri Yönetimi ağ geçidi**: Data Factory hizmeti destekler tooon içi verilere bağlanma (SAP Business Warehouse dahil) depoları bir bileşeni kullanılarak veri yönetimi ağ geçidi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="ebfd5-114">Veri Yönetimi ağ geçidi ve hello ağ geçidi, kurmak için adım adım yönergeler hakkında toolearn bkz [şirket içi veri arasında taşıma verilerini depolamak toocloud veri deposu](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="ebfd5-115">Bir Azure Iaas sanal makine (VM) Hello SAP Business Warehouse barındırılan olsa bile ağ geçidi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-115">Gateway is required even if hello SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="ebfd5-116">Merhaba ağ geçidi üzerinde aynı VM hello veri olarak depolamak veya hello ağ geçidi olarak aynı uzunlukta farklı bir VM üzerinde toohello veritabanı bağlanabilir hello yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="ebfd5-117">**SAP NetWeaver Kitaplığı** hello gateway makinesinde.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-117">**SAP NetWeaver library** on hello gateway machine.</span></span> <span data-ttu-id="ebfd5-118">SAP yöneticinizin veya doğrudan hello hello SAP Netweaver kitaplığı alabilirsiniz [SAP yazılım İndirme Merkezi](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="ebfd5-118">You can get hello SAP Netweaver library from your SAP administrator, or directly from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="ebfd5-119">Merhaba Ara **SAP Not #1025361** hello en son sürüm için tooget hello indirme konumu.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-119">Search for hello **SAP Note #1025361** tooget hello download location for hello most recent version.</span></span> <span data-ttu-id="ebfd5-120">Merhaba mimarisi hello SAP NetWeaver kitaplığı (32 bit veya 64 bit) için ağ geçidi yüklemenizi eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-120">Make sure that hello architecture for hello SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="ebfd5-121">Daha sonra hello SAP NetWeaver RFC SDK according toohello içinde SAP Not içerdiği tüm dosyaların yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-121">Then install all files included in hello SAP NetWeaver RFC SDK according toohello SAP Note.</span></span> <span data-ttu-id="ebfd5-122">Merhaba SAP NetWeaver kitaplığı hello SAP istemci araçlarını yükleme de dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-122">hello SAP NetWeaver library is also included in hello SAP Client Tools installation.</span></span>

> [!TIP]
> <span data-ttu-id="ebfd5-123">Merhaba NetWeaver RFC SDK system32 klasörüne ayıklanan hello DLL'leri yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-123">Put hello dlls extracted from hello NetWeaver RFC SDK into system32 folder.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ebfd5-124">Başlarken</span><span class="sxs-lookup"><span data-stu-id="ebfd5-124">Getting started</span></span>
<span data-ttu-id="ebfd5-125">Farklı araçlar/API'lerini kullanarak bir şirket içi Cassandra veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="ebfd5-126">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-126">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="ebfd5-127">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="ebfd5-128">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-128">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ebfd5-129">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="ebfd5-130">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ebfd5-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="ebfd5-131">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="ebfd5-132">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="ebfd5-133">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="ebfd5-134">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="ebfd5-135">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="ebfd5-136">Bir şirket içi SAP Business Warehouse kullanılan toocopy veri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: Blob SAP Business Warehouse tooAzure veri kopyalama](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse tooAzure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="ebfd5-137">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooan SAP BW veri deposu olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="ebfd5-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="ebfd5-138">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="ebfd5-138">Linked service properties</span></span>
<span data-ttu-id="ebfd5-139">Aşağıdaki tablonun hello JSON öğeleri belirli tooSAP iş ambar (BW) bağlantılı hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-139">hello following table provides description for JSON elements specific tooSAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="ebfd5-140">Özellik</span><span class="sxs-lookup"><span data-stu-id="ebfd5-140">Property</span></span> | <span data-ttu-id="ebfd5-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ebfd5-141">Description</span></span> | <span data-ttu-id="ebfd5-142">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="ebfd5-142">Allowed values</span></span> | <span data-ttu-id="ebfd5-143">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ebfd5-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="ebfd5-144">sunucu</span><span class="sxs-lookup"><span data-stu-id="ebfd5-144">server</span></span> | <span data-ttu-id="ebfd5-145">Hangi hello SAP BW örneği bulunduğu hello sunucusunun adı.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-145">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="ebfd5-146">Dize</span><span class="sxs-lookup"><span data-stu-id="ebfd5-146">string</span></span> | <span data-ttu-id="ebfd5-147">Evet</span><span class="sxs-lookup"><span data-stu-id="ebfd5-147">Yes</span></span>
<span data-ttu-id="ebfd5-148">systemNumber</span><span class="sxs-lookup"><span data-stu-id="ebfd5-148">systemNumber</span></span> | <span data-ttu-id="ebfd5-149">SAP BW sistem hello sistem sayısı.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-149">System number of hello SAP BW system.</span></span> | <span data-ttu-id="ebfd5-150">Bir dize olarak gösterilen iki basamaklı ondalık sayı.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-150">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="ebfd5-151">Evet</span><span class="sxs-lookup"><span data-stu-id="ebfd5-151">Yes</span></span>
<span data-ttu-id="ebfd5-152">istemci kimliği</span><span class="sxs-lookup"><span data-stu-id="ebfd5-152">clientId</span></span> | <span data-ttu-id="ebfd5-153">Merhaba SAP W sistem hello istemcisinde istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-153">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="ebfd5-154">Bir dize olarak gösterilen üç basamaklı ondalık sayı.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-154">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="ebfd5-155">Evet</span><span class="sxs-lookup"><span data-stu-id="ebfd5-155">Yes</span></span>
<span data-ttu-id="ebfd5-156">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="ebfd5-156">username</span></span> | <span data-ttu-id="ebfd5-157">Erişim toohello SAP sunucusuna sahip hello kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="ebfd5-157">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="ebfd5-158">Dize</span><span class="sxs-lookup"><span data-stu-id="ebfd5-158">string</span></span> | <span data-ttu-id="ebfd5-159">Evet</span><span class="sxs-lookup"><span data-stu-id="ebfd5-159">Yes</span></span>
<span data-ttu-id="ebfd5-160">password</span><span class="sxs-lookup"><span data-stu-id="ebfd5-160">password</span></span> | <span data-ttu-id="ebfd5-161">Merhaba kullanıcının parolası.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-161">Password for hello user.</span></span> | <span data-ttu-id="ebfd5-162">Dize</span><span class="sxs-lookup"><span data-stu-id="ebfd5-162">string</span></span> | <span data-ttu-id="ebfd5-163">Evet</span><span class="sxs-lookup"><span data-stu-id="ebfd5-163">Yes</span></span>
<span data-ttu-id="ebfd5-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ebfd5-164">gatewayName</span></span> | <span data-ttu-id="ebfd5-165">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi SAP BW örneğini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-165">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="ebfd5-166">Dize</span><span class="sxs-lookup"><span data-stu-id="ebfd5-166">string</span></span> | <span data-ttu-id="ebfd5-167">Evet</span><span class="sxs-lookup"><span data-stu-id="ebfd5-167">Yes</span></span>
<span data-ttu-id="ebfd5-168">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="ebfd5-168">encryptedCredential</span></span> | <span data-ttu-id="ebfd5-169">şifrelenmiş hello kimlik dizesi.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-169">hello encrypted credential string.</span></span> | <span data-ttu-id="ebfd5-170">Dize</span><span class="sxs-lookup"><span data-stu-id="ebfd5-170">string</span></span> | <span data-ttu-id="ebfd5-171">Hayır</span><span class="sxs-lookup"><span data-stu-id="ebfd5-171">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="ebfd5-172">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="ebfd5-172">Dataset properties</span></span>
<span data-ttu-id="ebfd5-173">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="ebfd5-174">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="ebfd5-175">Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-175">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="ebfd5-176">Merhaba SAP BW veri kümesi türü için desteklenen türüne özgü özellikler yok **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-176">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="ebfd5-177">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="ebfd5-177">Copy activity properties</span></span>
<span data-ttu-id="ebfd5-178">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-178">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ebfd5-179">Ad, açıklama, giriş ve çıkış tabloları gibi özellikleri olan ilkeleri etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-179">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="ebfd5-180">Oysa hello kullanılabilen özellikleri **typeProperties** hello etkinlik bölümünü her etkinlik türü ile değişir.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-180">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="ebfd5-181">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-181">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="ebfd5-182">Kopyalama etkinliği kaynağında türü olduğunda **RelationalSource** (içeren SAP BW), aşağıdaki özelliklere hello typeProperties bölümünde bulunur:</span><span class="sxs-lookup"><span data-stu-id="ebfd5-182">When source in copy activity is of type **RelationalSource** (which includes SAP BW), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="ebfd5-183">Özellik</span><span class="sxs-lookup"><span data-stu-id="ebfd5-183">Property</span></span> | <span data-ttu-id="ebfd5-184">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ebfd5-184">Description</span></span> | <span data-ttu-id="ebfd5-185">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="ebfd5-185">Allowed values</span></span> | <span data-ttu-id="ebfd5-186">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ebfd5-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ebfd5-187">sorgu</span><span class="sxs-lookup"><span data-stu-id="ebfd5-187">query</span></span> | <span data-ttu-id="ebfd5-188">Merhaba MDX Sorgusu tooread veri hello SAP BW örneğinden belirtir.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-188">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="ebfd5-189">MDX Sorgusu.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-189">MDX query.</span></span> | <span data-ttu-id="ebfd5-190">Evet</span><span class="sxs-lookup"><span data-stu-id="ebfd5-190">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-tooazure-blob"></a><span data-ttu-id="ebfd5-191">JSON örnek: Blob SAP Business Warehouse tooAzure veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="ebfd5-191">JSON example: Copy data from SAP Business Warehouse tooAzure Blob</span></span>
<span data-ttu-id="ebfd5-192">Merhaba aşağıdaki örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ebfd5-192">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="ebfd5-193">Bu örnek göstermektedir nasıl bir şirket içi SAP Business Warehouse tooan Azure Blob Storage toocopy verileri.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-193">This sample shows how toocopy data from an on-premises SAP Business Warehouse tooan Azure Blob Storage.</span></span> <span data-ttu-id="ebfd5-194">Ancak, veriler kopyalanabilir **doğrudan** belirtildiği hello havuzlarını tooany [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-194">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="ebfd5-195">Bu örnek, JSON parçacıklarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-195">This sample provides JSON snippets.</span></span> <span data-ttu-id="ebfd5-196">Merhaba veri fabrikası oluşturma için yönergeler içermez.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-196">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="ebfd5-197">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-197">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="ebfd5-198">Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="ebfd5-198">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="ebfd5-199">Bağlı hizmet türü [SapBw](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ebfd5-199">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="ebfd5-200">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ebfd5-200">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ebfd5-201">Bir giriş [dataset](data-factory-create-datasets.md) türü [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ebfd5-201">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="ebfd5-202">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ebfd5-202">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="ebfd5-203">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ebfd5-203">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="ebfd5-204">Merhaba örnek verileri saatte bir SAP Business Warehouse örneği tooan Azure blob kopyalar.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-204">hello sample copies data from an SAP Business Warehouse instance tooan Azure blob hourly.</span></span> <span data-ttu-id="ebfd5-205">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-205">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="ebfd5-206">İlk adım olarak, hello veri yönetimi ağ geçidi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-206">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="ebfd5-207">Merhaba yönergelerdir hello [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-207">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="ebfd5-208">SAP Business Warehouse hizmeti bağlı</span><span class="sxs-lookup"><span data-stu-id="ebfd5-208">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="ebfd5-209">SAP BW örneği toohello data factory'nizi hizmet bağlantıları bağlanmış.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-209">This linked service links your SAP BW instance toohello data factory.</span></span> <span data-ttu-id="ebfd5-210">Merhaba type özelliği çok ayarlamak**SapBw**.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-210">hello type property is set too**SapBw**.</span></span> <span data-ttu-id="ebfd5-211">Merhaba typeProperties bölüm hello SAP BW örneği için bağlantı bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-211">hello typeProperties section provides connection information for hello SAP BW instance.</span></span> 

```json
{
    "name": "SapBwLinkedService",
    "properties":
    {
        "type": "SapBw",
        "typeProperties":
        {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="ebfd5-212">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="ebfd5-212">Azure Storage linked service</span></span>
<span data-ttu-id="ebfd5-213">Bu hizmeti Azure Storage hesabı toohello data factory'nizi bağlı.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-213">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="ebfd5-214">Merhaba type özelliği çok ayarlamak**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-214">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="ebfd5-215">Merhaba typeProperties bölüm hello Azure depolama hesabı bağlantı bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-215">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="ebfd5-216">SAP BW girdi veri kümesi</span><span class="sxs-lookup"><span data-stu-id="ebfd5-216">SAP BW input dataset</span></span>
<span data-ttu-id="ebfd5-217">Bu veri kümesi hello SAP Business Warehouse veri kümesini tanımlamaktadır.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-217">This dataset defines hello SAP Business Warehouse dataset.</span></span> <span data-ttu-id="ebfd5-218">Merhaba Data Factory veri kümesi hello türü çok ayarlamak**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-218">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="ebfd5-219">Şu anda bir SAP BW veri kümesi için herhangi bir türe özgü özelliği belirtmeyin.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-219">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="ebfd5-220">Merhaba kopyalama etkinliği tanımı Hello sorguda hangi veri tooread hello SAP BW örneğinden belirtir.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-220">hello query in hello Copy Activity definition specifies what data tooread from hello SAP BW instance.</span></span> 

<span data-ttu-id="ebfd5-221">Dış özellik tootrue ayarı hello Data Factory hizmetinin bu hello tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil bildirir.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-221">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="ebfd5-222">Sıklık ve aralığı özelliklerini hello zamanlama tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-222">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="ebfd5-223">Bu durumda, hello veri hello SAP BW örneğinden saatlik okunur.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-223">In this case, hello data is read from hello SAP BW instance hourly.</span></span> 

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="ebfd5-224">Azure Blob çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="ebfd5-224">Azure Blob output dataset</span></span>
<span data-ttu-id="ebfd5-225">Bu veri kümesi hello çıktı Azure Blob dataset tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-225">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="ebfd5-226">Merhaba type özelliği tooAzureBlob ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-226">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="ebfd5-227">Merhaba typeProperties bölüm hello SAP BW örneğinden kopyalanan hello verilerinin depolandığı sağlar.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-227">hello typeProperties section provides where hello data copied from hello SAP BW instance is stored.</span></span> <span data-ttu-id="ebfd5-228">Merhaba veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="ebfd5-228">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ebfd5-229">hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="ebfd5-230">Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-230">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sapbw/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="ebfd5-231">Kopyalama etkinliği ile kanalı</span><span class="sxs-lookup"><span data-stu-id="ebfd5-231">Pipeline with Copy activity</span></span>
<span data-ttu-id="ebfd5-232">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-232">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="ebfd5-233">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**RelationalSource** (SAP BW kaynağı için) ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-233">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP BW source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="ebfd5-234">Merhaba belirtilen hello sorgu **sorgu** özelliği saat toocopy geçmiş hello hello veri seçer.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-234">hello query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<MDX query for SAP BW>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapBwDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapBwToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="ebfd5-235">SAP BW için tür eşlemesi</span><span class="sxs-lookup"><span data-stu-id="ebfd5-235">Type mapping for SAP BW</span></span>
<span data-ttu-id="ebfd5-236">Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri iki aşamalı bir yaklaşım aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="ebfd5-236">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="ebfd5-237">Yerel kaynak türleri too.NET türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="ebfd5-237">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="ebfd5-238">.NET türü toonative havuz türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="ebfd5-238">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="ebfd5-239">SAP BW verilerin taşınması, eşlemeleri aşağıdaki hello SAP BW türleri too.NET türlerinden kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-239">When moving data from SAP BW, hello following mappings are used from SAP BW types too.NET types.</span></span>

<span data-ttu-id="ebfd5-240">Merhaba ABAP sözlük veri türü</span><span class="sxs-lookup"><span data-stu-id="ebfd5-240">Data type in hello ABAP Dictionary</span></span> | <span data-ttu-id="ebfd5-241">.NET veri türü</span><span class="sxs-lookup"><span data-stu-id="ebfd5-241">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="ebfd5-242">ACCP</span><span class="sxs-lookup"><span data-stu-id="ebfd5-242">ACCP</span></span> |  <span data-ttu-id="ebfd5-243">Int</span><span class="sxs-lookup"><span data-stu-id="ebfd5-243">Int</span></span>
<span data-ttu-id="ebfd5-244">CHAR</span><span class="sxs-lookup"><span data-stu-id="ebfd5-244">CHAR</span></span> | <span data-ttu-id="ebfd5-245">Dize</span><span class="sxs-lookup"><span data-stu-id="ebfd5-245">String</span></span>
<span data-ttu-id="ebfd5-246">CLNT</span><span class="sxs-lookup"><span data-stu-id="ebfd5-246">CLNT</span></span> | <span data-ttu-id="ebfd5-247">Dize</span><span class="sxs-lookup"><span data-stu-id="ebfd5-247">String</span></span>
<span data-ttu-id="ebfd5-248">PB</span><span class="sxs-lookup"><span data-stu-id="ebfd5-248">CURR</span></span> | <span data-ttu-id="ebfd5-249">Ondalık</span><span class="sxs-lookup"><span data-stu-id="ebfd5-249">Decimal</span></span>
<span data-ttu-id="ebfd5-250">CUKY</span><span class="sxs-lookup"><span data-stu-id="ebfd5-250">CUKY</span></span> | <span data-ttu-id="ebfd5-251">Dize</span><span class="sxs-lookup"><span data-stu-id="ebfd5-251">String</span></span>
<span data-ttu-id="ebfd5-252">ARA</span><span class="sxs-lookup"><span data-stu-id="ebfd5-252">DEC</span></span> | <span data-ttu-id="ebfd5-253">Ondalık</span><span class="sxs-lookup"><span data-stu-id="ebfd5-253">Decimal</span></span>
<span data-ttu-id="ebfd5-254">FLTP</span><span class="sxs-lookup"><span data-stu-id="ebfd5-254">FLTP</span></span> | <span data-ttu-id="ebfd5-255">Çift</span><span class="sxs-lookup"><span data-stu-id="ebfd5-255">Double</span></span>
<span data-ttu-id="ebfd5-256">INT1</span><span class="sxs-lookup"><span data-stu-id="ebfd5-256">INT1</span></span> | <span data-ttu-id="ebfd5-257">Bayt</span><span class="sxs-lookup"><span data-stu-id="ebfd5-257">Byte</span></span>
<span data-ttu-id="ebfd5-258">INT2</span><span class="sxs-lookup"><span data-stu-id="ebfd5-258">INT2</span></span> | <span data-ttu-id="ebfd5-259">Int16</span><span class="sxs-lookup"><span data-stu-id="ebfd5-259">Int16</span></span>
<span data-ttu-id="ebfd5-260">INT4</span><span class="sxs-lookup"><span data-stu-id="ebfd5-260">INT4</span></span> | <span data-ttu-id="ebfd5-261">Int</span><span class="sxs-lookup"><span data-stu-id="ebfd5-261">Int</span></span>
<span data-ttu-id="ebfd5-262">DİL</span><span class="sxs-lookup"><span data-stu-id="ebfd5-262">LANG</span></span> | <span data-ttu-id="ebfd5-263">Dize</span><span class="sxs-lookup"><span data-stu-id="ebfd5-263">String</span></span>
<span data-ttu-id="ebfd5-264">LCHR</span><span class="sxs-lookup"><span data-stu-id="ebfd5-264">LCHR</span></span> | <span data-ttu-id="ebfd5-265">Dize</span><span class="sxs-lookup"><span data-stu-id="ebfd5-265">String</span></span>
<span data-ttu-id="ebfd5-266">LRAW</span><span class="sxs-lookup"><span data-stu-id="ebfd5-266">LRAW</span></span> | <span data-ttu-id="ebfd5-267">Byte]</span><span class="sxs-lookup"><span data-stu-id="ebfd5-267">Byte[]</span></span>
<span data-ttu-id="ebfd5-268">PREC</span><span class="sxs-lookup"><span data-stu-id="ebfd5-268">PREC</span></span> | <span data-ttu-id="ebfd5-269">Int16</span><span class="sxs-lookup"><span data-stu-id="ebfd5-269">Int16</span></span>
<span data-ttu-id="ebfd5-270">QUAN</span><span class="sxs-lookup"><span data-stu-id="ebfd5-270">QUAN</span></span> | <span data-ttu-id="ebfd5-271">Ondalık</span><span class="sxs-lookup"><span data-stu-id="ebfd5-271">Decimal</span></span>
<span data-ttu-id="ebfd5-272">HAM</span><span class="sxs-lookup"><span data-stu-id="ebfd5-272">RAW</span></span> | <span data-ttu-id="ebfd5-273">Byte]</span><span class="sxs-lookup"><span data-stu-id="ebfd5-273">Byte[]</span></span>
<span data-ttu-id="ebfd5-274">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="ebfd5-274">RAWSTRING</span></span> | <span data-ttu-id="ebfd5-275">Byte]</span><span class="sxs-lookup"><span data-stu-id="ebfd5-275">Byte[]</span></span>
<span data-ttu-id="ebfd5-276">DİZE</span><span class="sxs-lookup"><span data-stu-id="ebfd5-276">STRING</span></span> | <span data-ttu-id="ebfd5-277">Dize</span><span class="sxs-lookup"><span data-stu-id="ebfd5-277">String</span></span>
<span data-ttu-id="ebfd5-278">BİRİM</span><span class="sxs-lookup"><span data-stu-id="ebfd5-278">UNIT</span></span> | <span data-ttu-id="ebfd5-279">Dize</span><span class="sxs-lookup"><span data-stu-id="ebfd5-279">String</span></span>
<span data-ttu-id="ebfd5-280">DATS</span><span class="sxs-lookup"><span data-stu-id="ebfd5-280">DATS</span></span> | <span data-ttu-id="ebfd5-281">Dize</span><span class="sxs-lookup"><span data-stu-id="ebfd5-281">String</span></span>
<span data-ttu-id="ebfd5-282">NUMC</span><span class="sxs-lookup"><span data-stu-id="ebfd5-282">NUMC</span></span> | <span data-ttu-id="ebfd5-283">Dize</span><span class="sxs-lookup"><span data-stu-id="ebfd5-283">String</span></span>
<span data-ttu-id="ebfd5-284">TIMS</span><span class="sxs-lookup"><span data-stu-id="ebfd5-284">TIMS</span></span> | <span data-ttu-id="ebfd5-285">Dize</span><span class="sxs-lookup"><span data-stu-id="ebfd5-285">String</span></span>

> [!NOTE]
> <span data-ttu-id="ebfd5-286">Kaynak veri kümesi toocolumns havuz kümesinden toomap sütunlarından bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="ebfd5-286">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-toosink-columns"></a><span data-ttu-id="ebfd5-287">Kaynak toosink sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="ebfd5-287">Map source toosink columns</span></span>
<span data-ttu-id="ebfd5-288">Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="ebfd5-288">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="ebfd5-289">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="ebfd5-289">Repeatable read from relational sources</span></span>
<span data-ttu-id="ebfd5-290">İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-290">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="ebfd5-291">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-291">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="ebfd5-292">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-292">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="ebfd5-293">Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-293">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="ebfd5-294">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="ebfd5-294">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="ebfd5-295">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="ebfd5-295">Performance and Tuning</span></span>
<span data-ttu-id="ebfd5-296">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="ebfd5-296">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
