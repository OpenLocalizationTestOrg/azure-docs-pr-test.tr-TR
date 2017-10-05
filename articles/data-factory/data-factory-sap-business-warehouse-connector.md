---
title: "Azure Data Factory kullanarak SAP Business Warehouse veri taşıma | Microsoft Docs"
description: "Azure Data Factory kullanarak SAP Business Warehouse veri taşıma hakkında bilgi edinin."
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
ms.openlocfilehash: 220ccc8b94797880d335385046001c5f3b17c862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="bb698-103">Veri alanından SAP Business Azure Data Factory kullanarak ambar taşıma</span><span class="sxs-lookup"><span data-stu-id="bb698-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="bb698-104">Bu makalede kopya etkinliği Azure Data Factory'de bir şirket içi SAP Business Warehouse (BW) gelen verileri taşımak için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="bb698-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="bb698-105">Derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) kopyalama etkinliği ile veri taşıma için genel bir bakış sunar makalesi.</span><span class="sxs-lookup"><span data-stu-id="bb698-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="bb698-106">Bir şirket içi SAP Business Warehouse veri deposundan verileri herhangi bir desteklenen havuz veri deposuna kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb698-106">You can copy data from an on-premises SAP Business Warehouse data store to any supported sink data store.</span></span> <span data-ttu-id="bb698-107">Veri depoları havuzlarını kopyalama etkinliği tarafından desteklenen bir listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="bb698-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="bb698-108">Veri Fabrikası şu anda yalnızca taşıma verilerden bir SAP Business Warehouse diğer veri depolarına, ancak verileri diğer veri depolarına bir SAP Business Warehouse taşıma değil destekler.</span><span class="sxs-lookup"><span data-stu-id="bb698-108">Data factory currently supports only moving data from an SAP Business Warehouse to other data stores, but not for moving data from other data stores to an SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="bb698-109">Desteklenen sürümleri ve yükleme</span><span class="sxs-lookup"><span data-stu-id="bb698-109">Supported versions and installation</span></span>
<span data-ttu-id="bb698-110">Bu bağlayıcı SAP Business Warehouse sürümünü destekleyen 7.x.</span><span class="sxs-lookup"><span data-stu-id="bb698-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="bb698-111">MDX sorguları kullanarak veri kopyalamayı Infocubes ve QueryCubes (dahil olmak üzere BEx sorgular) destekler.</span><span class="sxs-lookup"><span data-stu-id="bb698-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="bb698-112">SAP BW örneği bağlantıyı etkinleştirmek için aşağıdaki bileşenleri yükleyin:</span><span class="sxs-lookup"><span data-stu-id="bb698-112">To enable the connectivity to the SAP BW instance, install the following components:</span></span>
- <span data-ttu-id="bb698-113">**Veri Yönetimi ağ geçidi**: Data Factory hizmeti desteklediği şirket içi verilere bağlanma (SAP Business Warehouse dahil) depoları bir bileşeni kullanılarak veri yönetimi ağ geçidi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="bb698-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="bb698-114">Veri Yönetimi ağ geçidi ve adım adım yönergeler için ağ geçidi ayarlama hakkında bilgi edinmek için [şirket içi veri arasında taşıma verilerini depolamak veri deposu buluta](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="bb698-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="bb698-115">SAP Business Warehouse bir Azure Iaas sanal makine (VM) barındırılan olsa bile ağ geçidi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="bb698-115">Gateway is required even if the SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="bb698-116">Ağ geçidi veritabanına bağlanıp sürece veri deposu olarak aynı VM veya farklı bir VM ağ geçidi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb698-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="bb698-117">**SAP NetWeaver Kitaplığı** ağ geçidi bilgisayarında.</span><span class="sxs-lookup"><span data-stu-id="bb698-117">**SAP NetWeaver library** on the gateway machine.</span></span> <span data-ttu-id="bb698-118">SAP Netweaver kitaplığı SAP yöneticinizden ya da doğrudan alabilirsiniz [SAP yazılım İndirme Merkezi](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="bb698-118">You can get the SAP Netweaver library from your SAP administrator, or directly from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="bb698-119">Arama **SAP Not #1025361** en son sürümü karşıdan yükleme konumu alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="bb698-119">Search for the **SAP Note #1025361** to get the download location for the most recent version.</span></span> <span data-ttu-id="bb698-120">SAP NetWeaver kitaplığı (32 bit veya 64 bit) için Mimari, ağ geçidi yüklemenizi eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="bb698-120">Make sure that the architecture for the SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="bb698-121">Daha sonra SAP Not göre SAP NetWeaver RFC SDK'sı bulunan tüm dosyaları yükleyin.</span><span class="sxs-lookup"><span data-stu-id="bb698-121">Then install all files included in the SAP NetWeaver RFC SDK according to the SAP Note.</span></span> <span data-ttu-id="bb698-122">SAP NetWeaver kitaplığı SAP istemci araçlarını yükleme de dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="bb698-122">The SAP NetWeaver library is also included in the SAP Client Tools installation.</span></span>

> [!TIP]
> <span data-ttu-id="bb698-123">NetWeaver RFC SDK'dan system32 klasörüne ayıklanan DLL'leri yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="bb698-123">Put the dlls extracted from the NetWeaver RFC SDK into system32 folder.</span></span>

## <a name="getting-started"></a><span data-ttu-id="bb698-124">Başlarken</span><span class="sxs-lookup"><span data-stu-id="bb698-124">Getting started</span></span>
<span data-ttu-id="bb698-125">Farklı araçlar/API'lerini kullanarak bir şirket içi Cassandra veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bb698-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="bb698-126">Bir işlem hattı oluşturmak için en kolay yolu kullanmaktır **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="bb698-126">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="bb698-127">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) veri kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="bb698-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="bb698-128">Bir işlem hattı oluşturmak için aşağıdaki araçları kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu**, **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="bb698-128">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="bb698-129">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="bb698-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="bb698-130">Araçlar ya da API'leri kullanıp bir havuz veri deposu için bir kaynak veri deposundan verileri taşır bir ardışık düzen oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bb698-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="bb698-131">Oluşturma **bağlantılı Hizmetleri** girdi ve çıktı verilerini bağlamak için veri fabrikanıza depolar.</span><span class="sxs-lookup"><span data-stu-id="bb698-131">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="bb698-132">Oluşturma **veri kümeleri** kopyalama işlemi için girdi ve çıktı verilerini temsil etmek için.</span><span class="sxs-lookup"><span data-stu-id="bb698-132">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="bb698-133">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="bb698-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="bb698-134">Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bb698-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="bb698-135">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, JSON biçimini kullanarak bu Data Factory varlıklarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="bb698-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="bb698-136">Bir şirket içi SAP Business Warehouse verileri kopyalamak için kullanılan Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: veri kopyalama SAP Business Warehouse Azure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="bb698-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse to Azure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="bb698-137">Aşağıdaki bölümler, Data Factory varlıklarını belirli bir SAP BW veri deposuna tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="bb698-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="bb698-138">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="bb698-138">Linked service properties</span></span>
<span data-ttu-id="bb698-139">Aşağıdaki tabloda, JSON öğeleri SAP Business Warehouse (BW) bağlantılı hizmete özgü açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb698-139">The following table provides description for JSON elements specific to SAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="bb698-140">Özellik</span><span class="sxs-lookup"><span data-stu-id="bb698-140">Property</span></span> | <span data-ttu-id="bb698-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bb698-141">Description</span></span> | <span data-ttu-id="bb698-142">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="bb698-142">Allowed values</span></span> | <span data-ttu-id="bb698-143">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bb698-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="bb698-144">sunucu</span><span class="sxs-lookup"><span data-stu-id="bb698-144">server</span></span> | <span data-ttu-id="bb698-145">SAP BW örneği bulunduğu sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="bb698-145">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="bb698-146">Dize</span><span class="sxs-lookup"><span data-stu-id="bb698-146">string</span></span> | <span data-ttu-id="bb698-147">Evet</span><span class="sxs-lookup"><span data-stu-id="bb698-147">Yes</span></span>
<span data-ttu-id="bb698-148">systemNumber</span><span class="sxs-lookup"><span data-stu-id="bb698-148">systemNumber</span></span> | <span data-ttu-id="bb698-149">SAP BW sisteminin sistem numarası.</span><span class="sxs-lookup"><span data-stu-id="bb698-149">System number of the SAP BW system.</span></span> | <span data-ttu-id="bb698-150">Bir dize olarak gösterilen iki basamaklı ondalık sayı.</span><span class="sxs-lookup"><span data-stu-id="bb698-150">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="bb698-151">Evet</span><span class="sxs-lookup"><span data-stu-id="bb698-151">Yes</span></span>
<span data-ttu-id="bb698-152">istemci kimliği</span><span class="sxs-lookup"><span data-stu-id="bb698-152">clientId</span></span> | <span data-ttu-id="bb698-153">SAP W sistem istemcisinde istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="bb698-153">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="bb698-154">Bir dize olarak gösterilen üç basamaklı ondalık sayı.</span><span class="sxs-lookup"><span data-stu-id="bb698-154">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="bb698-155">Evet</span><span class="sxs-lookup"><span data-stu-id="bb698-155">Yes</span></span>
<span data-ttu-id="bb698-156">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="bb698-156">username</span></span> | <span data-ttu-id="bb698-157">SAP sunucusuna erişimi olan kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="bb698-157">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="bb698-158">Dize</span><span class="sxs-lookup"><span data-stu-id="bb698-158">string</span></span> | <span data-ttu-id="bb698-159">Evet</span><span class="sxs-lookup"><span data-stu-id="bb698-159">Yes</span></span>
<span data-ttu-id="bb698-160">password</span><span class="sxs-lookup"><span data-stu-id="bb698-160">password</span></span> | <span data-ttu-id="bb698-161">Kullanıcının parolası.</span><span class="sxs-lookup"><span data-stu-id="bb698-161">Password for the user.</span></span> | <span data-ttu-id="bb698-162">Dize</span><span class="sxs-lookup"><span data-stu-id="bb698-162">string</span></span> | <span data-ttu-id="bb698-163">Evet</span><span class="sxs-lookup"><span data-stu-id="bb698-163">Yes</span></span>
<span data-ttu-id="bb698-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="bb698-164">gatewayName</span></span> | <span data-ttu-id="bb698-165">Data Factory hizmetinin şirket içi SAP BW örneğine bağlanmak için kullanması gereken ağ geçidinin adı.</span><span class="sxs-lookup"><span data-stu-id="bb698-165">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="bb698-166">Dize</span><span class="sxs-lookup"><span data-stu-id="bb698-166">string</span></span> | <span data-ttu-id="bb698-167">Evet</span><span class="sxs-lookup"><span data-stu-id="bb698-167">Yes</span></span>
<span data-ttu-id="bb698-168">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="bb698-168">encryptedCredential</span></span> | <span data-ttu-id="bb698-169">Şifrelenmiş kimlik bilgileri dizesi.</span><span class="sxs-lookup"><span data-stu-id="bb698-169">The encrypted credential string.</span></span> | <span data-ttu-id="bb698-170">Dize</span><span class="sxs-lookup"><span data-stu-id="bb698-170">string</span></span> | <span data-ttu-id="bb698-171">Hayır</span><span class="sxs-lookup"><span data-stu-id="bb698-171">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="bb698-172">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="bb698-172">Dataset properties</span></span>
<span data-ttu-id="bb698-173">Bölümler & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="bb698-173">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="bb698-174">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="bb698-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="bb698-175">**TypeProperties** bölüm veri kümesi her tür için farklıdır ve verilerin veri deposunda konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb698-175">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="bb698-176">SAP BW veri kümesi türü için desteklenen türüne özgü özellikler yok **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="bb698-176">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="bb698-177">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="bb698-177">Copy activity properties</span></span>
<span data-ttu-id="bb698-178">Bölümler & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz: [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="bb698-178">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="bb698-179">Ad, açıklama, giriş ve çıkış tabloları gibi özellikleri olan ilkeleri etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bb698-179">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="bb698-180">Bulunan özellikler **typeProperties** etkinlik bölümünü her etkinlik türü ile değişir.</span><span class="sxs-lookup"><span data-stu-id="bb698-180">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="bb698-181">Kopya etkinliği için bunlar türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="bb698-181">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="bb698-182">Kopyalama etkinliği kaynağında türü olduğunda **RelationalSource** (içeren SAP BW), aşağıdaki özellikler typeProperties bölümünde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="bb698-182">When source in copy activity is of type **RelationalSource** (which includes SAP BW), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="bb698-183">Özellik</span><span class="sxs-lookup"><span data-stu-id="bb698-183">Property</span></span> | <span data-ttu-id="bb698-184">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bb698-184">Description</span></span> | <span data-ttu-id="bb698-185">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="bb698-185">Allowed values</span></span> | <span data-ttu-id="bb698-186">Gerekli</span><span class="sxs-lookup"><span data-stu-id="bb698-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bb698-187">sorgu</span><span class="sxs-lookup"><span data-stu-id="bb698-187">query</span></span> | <span data-ttu-id="bb698-188">SAP BW örneğinden verileri okumak için MDX Sorgusu belirtir.</span><span class="sxs-lookup"><span data-stu-id="bb698-188">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="bb698-189">MDX Sorgusu.</span><span class="sxs-lookup"><span data-stu-id="bb698-189">MDX query.</span></span> | <span data-ttu-id="bb698-190">Evet</span><span class="sxs-lookup"><span data-stu-id="bb698-190">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-to-azure-blob"></a><span data-ttu-id="bb698-191">JSON örnek: veri kopyalama SAP Business Warehouse Azure Blob</span><span class="sxs-lookup"><span data-stu-id="bb698-191">JSON example: Copy data from SAP Business Warehouse to Azure Blob</span></span>
<span data-ttu-id="bb698-192">Aşağıdaki örneği kullanarak bir işlem hattı oluşturmak için kullanabileceğiniz örnek JSON tanımları sağlar, [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bb698-192">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="bb698-193">Bu örnek, bir şirket içi SAP Business Warehouse bir Azure Blob depolama alanına veri kopyalama gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="bb698-193">This sample shows how to copy data from an on-premises SAP Business Warehouse to an Azure Blob Storage.</span></span> <span data-ttu-id="bb698-194">Ancak, veriler kopyalanabilir **doğrudan** belirtildiği havuzlarını hiçbirine [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kopya etkinliği Azure Data Factory kullanarak.</span><span class="sxs-lookup"><span data-stu-id="bb698-194">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="bb698-195">Bu örnek, JSON parçacıklarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb698-195">This sample provides JSON snippets.</span></span> <span data-ttu-id="bb698-196">Data factory oluşturmak için adım adım yönergeler içermez.</span><span class="sxs-lookup"><span data-stu-id="bb698-196">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="bb698-197">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="bb698-197">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="bb698-198">Örnek aşağıdaki data factory varlıklarını sahiptir:</span><span class="sxs-lookup"><span data-stu-id="bb698-198">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="bb698-199">Bağlı hizmet türü [SapBw](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bb698-199">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="bb698-200">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bb698-200">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="bb698-201">Bir giriş [dataset](data-factory-create-datasets.md) türü [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bb698-201">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="bb698-202">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bb698-202">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="bb698-203">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="bb698-203">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="bb698-204">Örnek verileri bir SAP Business Warehouse örneğinden bir Azure blob saatlik kopyalar.</span><span class="sxs-lookup"><span data-stu-id="bb698-204">The sample copies data from an SAP Business Warehouse instance to an Azure blob hourly.</span></span> <span data-ttu-id="bb698-205">Bu örnekler kullanılan JSON özellikleri örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="bb698-205">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="bb698-206">İlk adım olarak, veri yönetimi ağ geçidi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="bb698-206">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="bb698-207">Yönergeler bulunan [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="bb698-207">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="bb698-208">SAP Business Warehouse hizmeti bağlı</span><span class="sxs-lookup"><span data-stu-id="bb698-208">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="bb698-209">Bu hizmet bağlantılar, SAP BW data factory bağlı örneği.</span><span class="sxs-lookup"><span data-stu-id="bb698-209">This linked service links your SAP BW instance to the data factory.</span></span> <span data-ttu-id="bb698-210">Type özelliği ayarlamak **SapBw**.</span><span class="sxs-lookup"><span data-stu-id="bb698-210">The type property is set to **SapBw**.</span></span> <span data-ttu-id="bb698-211">TypeProperties bölüm SAP BW örneği için bağlantı bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb698-211">The typeProperties section provides connection information for the SAP BW instance.</span></span> 

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="bb698-212">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="bb698-212">Azure Storage linked service</span></span>
<span data-ttu-id="bb698-213">Bu hizmeti Azure Storage hesabınızı data factory bağlantılı.</span><span class="sxs-lookup"><span data-stu-id="bb698-213">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="bb698-214">Type özelliği ayarlamak **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="bb698-214">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="bb698-215">TypeProperties bölümünde Azure depolama hesabı için bağlantı bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb698-215">The typeProperties section provides connection information for the Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="bb698-216">SAP BW girdi veri kümesi</span><span class="sxs-lookup"><span data-stu-id="bb698-216">SAP BW input dataset</span></span>
<span data-ttu-id="bb698-217">Bu veri kümesi SAP Business Warehouse veri kümesini tanımlamaktadır.</span><span class="sxs-lookup"><span data-stu-id="bb698-217">This dataset defines the SAP Business Warehouse dataset.</span></span> <span data-ttu-id="bb698-218">Data Factory veri kümesi için türünü ayarlayın **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="bb698-218">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="bb698-219">Şu anda bir SAP BW veri kümesi için herhangi bir türe özgü özelliği belirtmeyin.</span><span class="sxs-lookup"><span data-stu-id="bb698-219">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="bb698-220">Kopyalama etkinliği tanımı sorguda SAP BW örneğinden okumak için hangi verilerin belirtir.</span><span class="sxs-lookup"><span data-stu-id="bb698-220">The query in the Copy Activity definition specifies what data to read from the SAP BW instance.</span></span> 

<span data-ttu-id="bb698-221">Dış özelliği true olarak ayarlanmasını Data Factory hizmetinin tablo data factory dış ve veri fabrikasında bir etkinlik tarafından üretilen değil bildirir.</span><span class="sxs-lookup"><span data-stu-id="bb698-221">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="bb698-222">Sıklık ve aralığı özelliklerini zamanlamayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="bb698-222">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="bb698-223">Bu durumda, veriler SAP BW örneğinden saatlik okunur.</span><span class="sxs-lookup"><span data-stu-id="bb698-223">In this case, the data is read from the SAP BW instance hourly.</span></span> 

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



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="bb698-224">Azure Blob çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="bb698-224">Azure Blob output dataset</span></span>
<span data-ttu-id="bb698-225">Bu veri kümesini çıktı Azure Blob dataset tanımlar.</span><span class="sxs-lookup"><span data-stu-id="bb698-225">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="bb698-226">Type özelliği AzureBlob olarak ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="bb698-226">The type property is set to AzureBlob.</span></span> <span data-ttu-id="bb698-227">SAP BW örneğinden kopyalanan verilerin depolandığı typeProperties bölüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb698-227">The typeProperties section provides where the data copied from the SAP BW instance is stored.</span></span> <span data-ttu-id="bb698-228">Veriler her saat yeni bir bloba yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="bb698-228">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="bb698-229">Blob klasör yolu dinamik işlenmekte olan dilim başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="bb698-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="bb698-230">Klasör yolu yıl, ay, gün ve saat bölümleri başlangıç saatini kullanır.</span><span class="sxs-lookup"><span data-stu-id="bb698-230">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="bb698-231">Kopyalama etkinliği ile kanalı</span><span class="sxs-lookup"><span data-stu-id="bb698-231">Pipeline with Copy activity</span></span>
<span data-ttu-id="bb698-232">Ardışık Düzen giriş ve çıkış veri kümeleri kullanmak üzere yapılandırıldığı ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="bb698-232">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="bb698-233">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **RelationalSource** (SAP BW kaynağı için) ve **havuz** türü ayarlanmış **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="bb698-233">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP BW source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="bb698-234">İçin belirtilen sorgu **sorgu** özelliği veri kopyalamak için son bir saat içindeki seçer.</span><span class="sxs-lookup"><span data-stu-id="bb698-234">The query specified for the **query** property selects the data in the past hour to copy.</span></span>

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



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="bb698-235">SAP BW için tür eşlemesi</span><span class="sxs-lookup"><span data-stu-id="bb698-235">Type mapping for SAP BW</span></span>
<span data-ttu-id="bb698-236">Bölümünde belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği, aşağıdaki iki aşamalı yaklaşımı türleriyle havuz için kaynak türünden otomatik tür dönüşümleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="bb698-236">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="bb698-237">Yerel kaynak türlerinden .NET türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="bb698-237">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="bb698-238">.NET türünden yerel havuz türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="bb698-238">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="bb698-239">SAP BW verilerin taşınması, aşağıdaki eşlemelerini SAP BW türlerinden .NET türleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bb698-239">When moving data from SAP BW, the following mappings are used from SAP BW types to .NET types.</span></span>

<span data-ttu-id="bb698-240">ABAP sözlükteki veri türü</span><span class="sxs-lookup"><span data-stu-id="bb698-240">Data type in the ABAP Dictionary</span></span> | <span data-ttu-id="bb698-241">.NET veri türü</span><span class="sxs-lookup"><span data-stu-id="bb698-241">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="bb698-242">ACCP</span><span class="sxs-lookup"><span data-stu-id="bb698-242">ACCP</span></span> |  <span data-ttu-id="bb698-243">Int</span><span class="sxs-lookup"><span data-stu-id="bb698-243">Int</span></span>
<span data-ttu-id="bb698-244">CHAR</span><span class="sxs-lookup"><span data-stu-id="bb698-244">CHAR</span></span> | <span data-ttu-id="bb698-245">Dize</span><span class="sxs-lookup"><span data-stu-id="bb698-245">String</span></span>
<span data-ttu-id="bb698-246">CLNT</span><span class="sxs-lookup"><span data-stu-id="bb698-246">CLNT</span></span> | <span data-ttu-id="bb698-247">Dize</span><span class="sxs-lookup"><span data-stu-id="bb698-247">String</span></span>
<span data-ttu-id="bb698-248">PB</span><span class="sxs-lookup"><span data-stu-id="bb698-248">CURR</span></span> | <span data-ttu-id="bb698-249">Ondalık</span><span class="sxs-lookup"><span data-stu-id="bb698-249">Decimal</span></span>
<span data-ttu-id="bb698-250">CUKY</span><span class="sxs-lookup"><span data-stu-id="bb698-250">CUKY</span></span> | <span data-ttu-id="bb698-251">Dize</span><span class="sxs-lookup"><span data-stu-id="bb698-251">String</span></span>
<span data-ttu-id="bb698-252">ARA</span><span class="sxs-lookup"><span data-stu-id="bb698-252">DEC</span></span> | <span data-ttu-id="bb698-253">Ondalık</span><span class="sxs-lookup"><span data-stu-id="bb698-253">Decimal</span></span>
<span data-ttu-id="bb698-254">FLTP</span><span class="sxs-lookup"><span data-stu-id="bb698-254">FLTP</span></span> | <span data-ttu-id="bb698-255">Çift</span><span class="sxs-lookup"><span data-stu-id="bb698-255">Double</span></span>
<span data-ttu-id="bb698-256">INT1</span><span class="sxs-lookup"><span data-stu-id="bb698-256">INT1</span></span> | <span data-ttu-id="bb698-257">Bayt</span><span class="sxs-lookup"><span data-stu-id="bb698-257">Byte</span></span>
<span data-ttu-id="bb698-258">INT2</span><span class="sxs-lookup"><span data-stu-id="bb698-258">INT2</span></span> | <span data-ttu-id="bb698-259">Int16</span><span class="sxs-lookup"><span data-stu-id="bb698-259">Int16</span></span>
<span data-ttu-id="bb698-260">INT4</span><span class="sxs-lookup"><span data-stu-id="bb698-260">INT4</span></span> | <span data-ttu-id="bb698-261">Int</span><span class="sxs-lookup"><span data-stu-id="bb698-261">Int</span></span>
<span data-ttu-id="bb698-262">DİL</span><span class="sxs-lookup"><span data-stu-id="bb698-262">LANG</span></span> | <span data-ttu-id="bb698-263">Dize</span><span class="sxs-lookup"><span data-stu-id="bb698-263">String</span></span>
<span data-ttu-id="bb698-264">LCHR</span><span class="sxs-lookup"><span data-stu-id="bb698-264">LCHR</span></span> | <span data-ttu-id="bb698-265">Dize</span><span class="sxs-lookup"><span data-stu-id="bb698-265">String</span></span>
<span data-ttu-id="bb698-266">LRAW</span><span class="sxs-lookup"><span data-stu-id="bb698-266">LRAW</span></span> | <span data-ttu-id="bb698-267">Byte]</span><span class="sxs-lookup"><span data-stu-id="bb698-267">Byte[]</span></span>
<span data-ttu-id="bb698-268">PREC</span><span class="sxs-lookup"><span data-stu-id="bb698-268">PREC</span></span> | <span data-ttu-id="bb698-269">Int16</span><span class="sxs-lookup"><span data-stu-id="bb698-269">Int16</span></span>
<span data-ttu-id="bb698-270">QUAN</span><span class="sxs-lookup"><span data-stu-id="bb698-270">QUAN</span></span> | <span data-ttu-id="bb698-271">Ondalık</span><span class="sxs-lookup"><span data-stu-id="bb698-271">Decimal</span></span>
<span data-ttu-id="bb698-272">HAM</span><span class="sxs-lookup"><span data-stu-id="bb698-272">RAW</span></span> | <span data-ttu-id="bb698-273">Byte]</span><span class="sxs-lookup"><span data-stu-id="bb698-273">Byte[]</span></span>
<span data-ttu-id="bb698-274">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="bb698-274">RAWSTRING</span></span> | <span data-ttu-id="bb698-275">Byte]</span><span class="sxs-lookup"><span data-stu-id="bb698-275">Byte[]</span></span>
<span data-ttu-id="bb698-276">DİZE</span><span class="sxs-lookup"><span data-stu-id="bb698-276">STRING</span></span> | <span data-ttu-id="bb698-277">Dize</span><span class="sxs-lookup"><span data-stu-id="bb698-277">String</span></span>
<span data-ttu-id="bb698-278">BİRİM</span><span class="sxs-lookup"><span data-stu-id="bb698-278">UNIT</span></span> | <span data-ttu-id="bb698-279">Dize</span><span class="sxs-lookup"><span data-stu-id="bb698-279">String</span></span>
<span data-ttu-id="bb698-280">DATS</span><span class="sxs-lookup"><span data-stu-id="bb698-280">DATS</span></span> | <span data-ttu-id="bb698-281">Dize</span><span class="sxs-lookup"><span data-stu-id="bb698-281">String</span></span>
<span data-ttu-id="bb698-282">NUMC</span><span class="sxs-lookup"><span data-stu-id="bb698-282">NUMC</span></span> | <span data-ttu-id="bb698-283">Dize</span><span class="sxs-lookup"><span data-stu-id="bb698-283">String</span></span>
<span data-ttu-id="bb698-284">TIMS</span><span class="sxs-lookup"><span data-stu-id="bb698-284">TIMS</span></span> | <span data-ttu-id="bb698-285">Dize</span><span class="sxs-lookup"><span data-stu-id="bb698-285">String</span></span>

> [!NOTE]
> <span data-ttu-id="bb698-286">Kaynak veri kümesi sütunlarından havuz kümesinden sütunlara eşlemek için bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="bb698-286">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-to-sink-columns"></a><span data-ttu-id="bb698-287">Kaynak havuzu sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="bb698-287">Map source to sink columns</span></span>
<span data-ttu-id="bb698-288">Havuz dataset sütunlara kaynak kümesindeki eşleme sütunları hakkında bilgi edinmek için [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="bb698-288">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="bb698-289">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="bb698-289">Repeatable read from relational sources</span></span>
<span data-ttu-id="bb698-290">İlişkisel veri kopyalama verileri depoladığında, Yinelenebilirlik istenmeyen sonuçları önlemek için göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="bb698-290">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="bb698-291">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb698-291">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="bb698-292">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb698-292">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="bb698-293">Bir dilim iki yolla yeniden çalıştırıldığında, aynı veri dilimi çalıştırmak kaç kez geçtiğinden bağımsız okuduğunuzdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bb698-293">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="bb698-294">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="bb698-294">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="bb698-295">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="bb698-295">Performance and Tuning</span></span>
<span data-ttu-id="bb698-296">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve onu en iyi duruma getirmek için çeşitli yollar etkisi performansını anahtar Etkenler hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="bb698-296">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
