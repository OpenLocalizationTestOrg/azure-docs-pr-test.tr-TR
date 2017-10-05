---
title: "Azure Data Factory kullanarak SAP HANA veri taşıma | Microsoft Docs"
description: "Azure Data Factory kullanarak SAP HANA veri taşıma hakkında bilgi edinin."
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
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 2ab488d82d24999a6231e40cb719715463c51d64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="3b9c6-103">Veri gelen SAP, HANA Azure Data Factory kullanarak Taşı</span><span class="sxs-lookup"><span data-stu-id="3b9c6-103">Move data From SAP HANA using Azure Data Factory</span></span>
<span data-ttu-id="3b9c6-104">Bu makalede kopya etkinliği Azure Data Factory'de bir şirket içi SAP HANA verileri taşımak için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP HANA.</span></span> <span data-ttu-id="3b9c6-105">Derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) kopyalama etkinliği ile veri taşıma için genel bir bakış sunar makalesi.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="3b9c6-106">Bir şirket içi SAP HANA veri deposundan verileri herhangi bir desteklenen havuz veri deposuna kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-106">You can copy data from an on-premises SAP HANA data store to any supported sink data store.</span></span> <span data-ttu-id="3b9c6-107">Veri depoları havuzlarını kopyalama etkinliği tarafından desteklenen bir listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="3b9c6-108">Veri Fabrikası şu anda yalnızca taşıma verilerden bir SAP HANA diğer veri depolarına, ancak verileri diğer veri depolarına bir SAP HANA taşıma değil destekler.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-108">Data factory currently supports only moving data from an SAP HANA to other data stores, but not for moving data from other data stores to an SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="3b9c6-109">Desteklenen sürümleri ve yükleme</span><span class="sxs-lookup"><span data-stu-id="3b9c6-109">Supported versions and installation</span></span>
<span data-ttu-id="3b9c6-110">Bu bağlayıcı SAP HANA veritabanına herhangi bir sürümünü destekler.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-110">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="3b9c6-111">HANA bilgi modeli (gibi Analitik ve hesaplama görünümleri) ve SQL sorgularını kullanarak satır/sütun tablolarından veri kopyalamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="3b9c6-112">SAP HANA örneği bağlantıyı etkinleştirmek için aşağıdaki bileşenleri yükleyin:</span><span class="sxs-lookup"><span data-stu-id="3b9c6-112">To enable the connectivity to the SAP HANA instance, install the following components:</span></span>
- <span data-ttu-id="3b9c6-113">**Veri Yönetimi ağ geçidi**: Data Factory hizmeti desteklediği şirket içi verilere bağlanma (SAP HANA dahil) depoları bir bileşeni kullanılarak veri yönetimi ağ geçidi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="3b9c6-114">Veri Yönetimi ağ geçidi ve adım adım yönergeler için ağ geçidi ayarlama hakkında bilgi edinmek için [şirket içi veri arasında taşıma verilerini depolamak veri deposu buluta](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="3b9c6-115">SAP HANA bir Azure Iaas sanal makine (VM) barındırılan olsa bile ağ geçidi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-115">Gateway is required even if the SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="3b9c6-116">Ağ geçidi veritabanına bağlanıp sürece veri deposu olarak aynı VM veya farklı bir VM ağ geçidi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="3b9c6-117">**SAP HANA ODBC sürücüsü** ağ geçidi bilgisayarında.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-117">**SAP HANA ODBC driver** on the gateway machine.</span></span> <span data-ttu-id="3b9c6-118">SAP HANA ODBC sürücüsünü yükleyebilirsiniz [SAP yazılım İndirme Merkezi](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="3b9c6-118">You can download the SAP HANA ODBC driver from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="3b9c6-119">Arama anahtar sözcüğü ile **Windows için SAP HANA İSTEMCİSİ**.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-119">Search with the keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="3b9c6-120">Başlarken</span><span class="sxs-lookup"><span data-stu-id="3b9c6-120">Getting started</span></span>
<span data-ttu-id="3b9c6-121">Farklı araçlar/API'lerini kullanarak bir şirket içi Cassandra veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="3b9c6-122">Bir işlem hattı oluşturmak için en kolay yolu kullanmaktır **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="3b9c6-123">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) veri kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="3b9c6-124">Bir işlem hattı oluşturmak için aşağıdaki araçları kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu**, **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="3b9c6-125">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="3b9c6-126">Araçlar ya da API'leri kullanıp bir havuz veri deposu için bir kaynak veri deposundan verileri taşır bir ardışık düzen oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3b9c6-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="3b9c6-127">Oluşturma **bağlantılı Hizmetleri** girdi ve çıktı verilerini bağlamak için veri fabrikanıza depolar.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-127">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="3b9c6-128">Oluşturma **veri kümeleri** kopyalama işlemi için girdi ve çıktı verilerini temsil etmek için.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-128">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="3b9c6-129">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="3b9c6-130">Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-130">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="3b9c6-131">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, JSON biçimini kullanarak bu Data Factory varlıklarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="3b9c6-132">Bir şirket içi SAP HANA veri kopyalamak için kullanılan Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: veri kopyalama SAP HANA Azure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-132">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA to Azure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="3b9c6-133">Aşağıdaki bölümler, Data Factory varlıklarını belirli bir SAP HANA veri deposuna tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="3b9c6-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="3b9c6-134">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="3b9c6-134">Linked service properties</span></span>
<span data-ttu-id="3b9c6-135">Aşağıdaki tabloda, JSON öğeleri SAP HANA bağlantılı hizmete özgü açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-135">The following table provides description for JSON elements specific to SAP HANA linked service.</span></span>

<span data-ttu-id="3b9c6-136">Özellik</span><span class="sxs-lookup"><span data-stu-id="3b9c6-136">Property</span></span> | <span data-ttu-id="3b9c6-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3b9c6-137">Description</span></span> | <span data-ttu-id="3b9c6-138">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="3b9c6-138">Allowed values</span></span> | <span data-ttu-id="3b9c6-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3b9c6-139">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="3b9c6-140">sunucu</span><span class="sxs-lookup"><span data-stu-id="3b9c6-140">server</span></span> | <span data-ttu-id="3b9c6-141">SAP HANA örneği bulunduğu sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-141">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="3b9c6-142">Sunucunuz özelleştirilmiş bir bağlantı noktası kullanıyorsa belirtin `server:port`.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-142">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="3b9c6-143">Dize</span><span class="sxs-lookup"><span data-stu-id="3b9c6-143">string</span></span> | <span data-ttu-id="3b9c6-144">Evet</span><span class="sxs-lookup"><span data-stu-id="3b9c6-144">Yes</span></span>
<span data-ttu-id="3b9c6-145">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3b9c6-145">authenticationType</span></span> | <span data-ttu-id="3b9c6-146">Kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-146">Type of authentication.</span></span> | <span data-ttu-id="3b9c6-147">Dize.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-147">string.</span></span> <span data-ttu-id="3b9c6-148">"Temel" veya "Windows"</span><span class="sxs-lookup"><span data-stu-id="3b9c6-148">"Basic" or "Windows"</span></span> | <span data-ttu-id="3b9c6-149">Evet</span><span class="sxs-lookup"><span data-stu-id="3b9c6-149">Yes</span></span> 
<span data-ttu-id="3b9c6-150">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="3b9c6-150">username</span></span> | <span data-ttu-id="3b9c6-151">SAP sunucusuna erişimi olan kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="3b9c6-151">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="3b9c6-152">Dize</span><span class="sxs-lookup"><span data-stu-id="3b9c6-152">string</span></span> | <span data-ttu-id="3b9c6-153">Evet</span><span class="sxs-lookup"><span data-stu-id="3b9c6-153">Yes</span></span>
<span data-ttu-id="3b9c6-154">password</span><span class="sxs-lookup"><span data-stu-id="3b9c6-154">password</span></span> | <span data-ttu-id="3b9c6-155">Kullanıcının parolası.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-155">Password for the user.</span></span> | <span data-ttu-id="3b9c6-156">Dize</span><span class="sxs-lookup"><span data-stu-id="3b9c6-156">string</span></span> | <span data-ttu-id="3b9c6-157">Evet</span><span class="sxs-lookup"><span data-stu-id="3b9c6-157">Yes</span></span>
<span data-ttu-id="3b9c6-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b9c6-158">gatewayName</span></span> | <span data-ttu-id="3b9c6-159">Data Factory hizmetinin şirket içi SAP HANA örneğine bağlanmak için kullanması gereken ağ geçidinin adı.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-159">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="3b9c6-160">Dize</span><span class="sxs-lookup"><span data-stu-id="3b9c6-160">string</span></span> | <span data-ttu-id="3b9c6-161">Evet</span><span class="sxs-lookup"><span data-stu-id="3b9c6-161">Yes</span></span>
<span data-ttu-id="3b9c6-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="3b9c6-162">encryptedCredential</span></span> | <span data-ttu-id="3b9c6-163">Şifrelenmiş kimlik bilgileri dizesi.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-163">The encrypted credential string.</span></span> | <span data-ttu-id="3b9c6-164">Dize</span><span class="sxs-lookup"><span data-stu-id="3b9c6-164">string</span></span> | <span data-ttu-id="3b9c6-165">Hayır</span><span class="sxs-lookup"><span data-stu-id="3b9c6-165">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="3b9c6-166">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="3b9c6-166">Dataset properties</span></span>
<span data-ttu-id="3b9c6-167">Bölümler & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-167">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="3b9c6-168">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="3b9c6-169">**TypeProperties** bölüm veri kümesi her tür için farklıdır ve verilerin veri deposunda konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-169">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="3b9c6-170">SAP HANA veri kümesi türü için desteklenen türüne özgü özellikler yok **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-170">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="3b9c6-171">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="3b9c6-171">Copy activity properties</span></span>
<span data-ttu-id="3b9c6-172">Bölümler & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz: [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-172">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="3b9c6-173">Ad, açıklama, giriş ve çıkış tabloları gibi özellikleri olan ilkeleri etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="3b9c6-174">Bulunan özellikler **typeProperties** etkinlik bölümünü her etkinlik türü ile değişir.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-174">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="3b9c6-175">Kopya etkinliği için bunlar türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-175">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="3b9c6-176">Kopyalama etkinliği kaynağında türü olduğunda **RelationalSource** (içeren SAP HANA), aşağıdaki özellikler typeProperties bölümünde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="3b9c6-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="3b9c6-177">Özellik</span><span class="sxs-lookup"><span data-stu-id="3b9c6-177">Property</span></span> | <span data-ttu-id="3b9c6-178">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3b9c6-178">Description</span></span> | <span data-ttu-id="3b9c6-179">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="3b9c6-179">Allowed values</span></span> | <span data-ttu-id="3b9c6-180">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3b9c6-180">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b9c6-181">sorgu</span><span class="sxs-lookup"><span data-stu-id="3b9c6-181">query</span></span> | <span data-ttu-id="3b9c6-182">SAP HANA örneğinden verileri okumak için SQL sorgusu belirtir.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-182">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="3b9c6-183">SQL sorgusu.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-183">SQL query.</span></span> | <span data-ttu-id="3b9c6-184">Evet</span><span class="sxs-lookup"><span data-stu-id="3b9c6-184">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-to-azure-blob"></a><span data-ttu-id="3b9c6-185">JSON örnek: veri kopyalama SAP HANA Azure Blob</span><span class="sxs-lookup"><span data-stu-id="3b9c6-185">JSON example: Copy data from SAP HANA to Azure Blob</span></span>
<span data-ttu-id="3b9c6-186">Aşağıdaki örneği kullanarak bir işlem hattı oluşturmak için kullanabileceğiniz örnek JSON tanımları sağlar, [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3b9c6-186">The following sample provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="3b9c6-187">Bu örnek, bir şirket içi SAP HANA bir Azure Blob depolama alanına veri kopyalama gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-187">This sample shows how to copy data from an on-premises SAP HANA to an Azure Blob Storage.</span></span> <span data-ttu-id="3b9c6-188">Ancak, veriler kopyalanabilir **doğrudan** listelenen herhangi havuzlarını [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kopya etkinliği Azure Data Factory kullanarak.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-188">However, data can be copied **directly** to any of the sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="3b9c6-189">Bu örnek, JSON parçacıklarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-189">This sample provides JSON snippets.</span></span> <span data-ttu-id="3b9c6-190">Data factory oluşturmak için adım adım yönergeler içermez.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-190">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="3b9c6-191">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="3b9c6-192">Örnek aşağıdaki data factory varlıklarını sahiptir:</span><span class="sxs-lookup"><span data-stu-id="3b9c6-192">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="3b9c6-193">Bağlı hizmet türü [SapHana](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3b9c6-193">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="3b9c6-194">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="3b9c6-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="3b9c6-195">Bir giriş [dataset](data-factory-create-datasets.md) türü [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3b9c6-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="3b9c6-196">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="3b9c6-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="3b9c6-197">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="3b9c6-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="3b9c6-198">Örnek verileri bir SAP HANA örnekten bir Azure blob saatlik kopyalar.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-198">The sample copies data from an SAP HANA instance to an Azure blob hourly.</span></span> <span data-ttu-id="3b9c6-199">Bu örnekler kullanılan JSON özellikleri örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="3b9c6-200">İlk adım olarak, veri yönetimi ağ geçidi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-200">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="3b9c6-201">Yönergeler bulunan [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="3b9c6-202">SAP HANA bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="3b9c6-202">SAP HANA linked service</span></span>
<span data-ttu-id="3b9c6-203">Bu hizmet bağlantılar, SAP HANA data factory bağlı örneği.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-203">This linked service links your SAP HANA instance to the data factory.</span></span> <span data-ttu-id="3b9c6-204">Type özelliği ayarlamak **SapHana**.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-204">The type property is set to **SapHana**.</span></span> <span data-ttu-id="3b9c6-205">TypeProperties bölüm SAP HANA örneği için bağlantı bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-205">The typeProperties section provides connection information for the SAP HANA instance.</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="3b9c6-206">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="3b9c6-206">Azure Storage linked service</span></span>
<span data-ttu-id="3b9c6-207">Bu hizmeti Azure Storage hesabınızı data factory bağlantılı.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-207">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="3b9c6-208">Type özelliği ayarlamak **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-208">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="3b9c6-209">TypeProperties bölümünde Azure depolama hesabı için bağlantı bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-209">The typeProperties section provides connection information for the Azure Storage account.</span></span>

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

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="3b9c6-210">SAP HANA giriş veri kümesi</span><span class="sxs-lookup"><span data-stu-id="3b9c6-210">SAP HANA input dataset</span></span>

<span data-ttu-id="3b9c6-211">Bu veri kümesi SAP HANA veri kümesini tanımlamaktadır.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-211">This dataset defines the SAP HANA dataset.</span></span> <span data-ttu-id="3b9c6-212">Data Factory veri kümesi için türünü ayarlayın **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-212">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="3b9c6-213">Şu anda, SAP HANA veri kümesi için herhangi bir türe özgü özelliği belirtmeyin.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="3b9c6-214">Kopyalama etkinliği tanımı sorguda SAP HANA örneğinden okumak için hangi verilerin belirtir.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-214">The query in the Copy Activity definition specifies what data to read from the SAP HANA instance.</span></span> 

<span data-ttu-id="3b9c6-215">Dış özelliği true olarak ayarlanmasını Data Factory hizmetinin tablo data factory dış ve veri fabrikasında bir etkinlik tarafından üretilen değil bildirir.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-215">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="3b9c6-216">Sıklık ve aralığı özelliklerini zamanlamayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-216">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="3b9c6-217">Bu durumda, veriler SAP HANA örnekten saatlik okunur.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-217">In this case, the data is read from the SAP HANA instance hourly.</span></span> 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="3b9c6-218">Azure Blob çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="3b9c6-218">Azure Blob output dataset</span></span>
<span data-ttu-id="3b9c6-219">Bu veri kümesini çıktı Azure Blob dataset tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-219">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="3b9c6-220">Type özelliği AzureBlob olarak ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-220">The type property is set to AzureBlob.</span></span> <span data-ttu-id="3b9c6-221">SAP HANA örneğinden kopyalanan verilerin depolandığı typeProperties bölüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-221">The typeProperties section provides where the data copied from the SAP HANA instance is stored.</span></span> <span data-ttu-id="3b9c6-222">Veriler her saat yeni bir bloba yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="3b9c6-222">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="3b9c6-223">Blob klasör yolu dinamik işlenmekte olan dilim başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-223">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="3b9c6-224">Klasör yolu yıl, ay, gün ve saat bölümleri başlangıç saatini kullanır.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-224">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="3b9c6-225">Kopyalama etkinliği ile kanalı</span><span class="sxs-lookup"><span data-stu-id="3b9c6-225">Pipeline with Copy activity</span></span>

<span data-ttu-id="3b9c6-226">Ardışık Düzen giriş ve çıkış veri kümeleri kullanmak üzere yapılandırıldığı ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-226">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="3b9c6-227">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **RelationalSource** (SAP HANA kaynağı için) ve **havuz** türü ayarlanmış **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-227">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP HANA source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="3b9c6-228">SQL sorgusu için belirtilen **sorgu** özelliği veri kopyalamak için son bir saat içindeki seçer.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-228">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
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
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="3b9c6-229">SAP HANA türü eşlemesi</span><span class="sxs-lookup"><span data-stu-id="3b9c6-229">Type mapping for SAP HANA</span></span>
<span data-ttu-id="3b9c6-230">Bölümünde belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği, aşağıdaki iki aşamalı yaklaşımı türleriyle havuz için kaynak türünden otomatik tür dönüşümleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="3b9c6-230">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="3b9c6-231">Yerel kaynak türlerinden .NET türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="3b9c6-231">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="3b9c6-232">.NET türünden yerel havuz türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="3b9c6-232">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="3b9c6-233">SAP HANA verilerin taşınması, aşağıdaki eşlemelerini SAP HANA türlerinden .NET türleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-233">When moving data from SAP HANA, the following mappings are used from SAP HANA types to .NET types.</span></span>

<span data-ttu-id="3b9c6-234">SAP HANA türü</span><span class="sxs-lookup"><span data-stu-id="3b9c6-234">SAP HANA Type</span></span> | <span data-ttu-id="3b9c6-235">.NET türü temelinde</span><span class="sxs-lookup"><span data-stu-id="3b9c6-235">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="3b9c6-236">MİNİ TAMSAYI</span><span class="sxs-lookup"><span data-stu-id="3b9c6-236">TINYINT</span></span> | <span data-ttu-id="3b9c6-237">Bayt</span><span class="sxs-lookup"><span data-stu-id="3b9c6-237">Byte</span></span>
<span data-ttu-id="3b9c6-238">TAMSAYI</span><span class="sxs-lookup"><span data-stu-id="3b9c6-238">SMALLINT</span></span> | <span data-ttu-id="3b9c6-239">Int16</span><span class="sxs-lookup"><span data-stu-id="3b9c6-239">Int16</span></span>
<span data-ttu-id="3b9c6-240">INT</span><span class="sxs-lookup"><span data-stu-id="3b9c6-240">INT</span></span> | <span data-ttu-id="3b9c6-241">Int32</span><span class="sxs-lookup"><span data-stu-id="3b9c6-241">Int32</span></span>
<span data-ttu-id="3b9c6-242">BIGINT</span><span class="sxs-lookup"><span data-stu-id="3b9c6-242">BIGINT</span></span> | <span data-ttu-id="3b9c6-243">Int64</span><span class="sxs-lookup"><span data-stu-id="3b9c6-243">Int64</span></span>
<span data-ttu-id="3b9c6-244">GERÇEK</span><span class="sxs-lookup"><span data-stu-id="3b9c6-244">REAL</span></span> | <span data-ttu-id="3b9c6-245">Tek</span><span class="sxs-lookup"><span data-stu-id="3b9c6-245">Single</span></span>
<span data-ttu-id="3b9c6-246">ÇİFT</span><span class="sxs-lookup"><span data-stu-id="3b9c6-246">DOUBLE</span></span> | <span data-ttu-id="3b9c6-247">Tek</span><span class="sxs-lookup"><span data-stu-id="3b9c6-247">Single</span></span>
<span data-ttu-id="3b9c6-248">ONDALIK</span><span class="sxs-lookup"><span data-stu-id="3b9c6-248">DECIMAL</span></span> | <span data-ttu-id="3b9c6-249">Ondalık</span><span class="sxs-lookup"><span data-stu-id="3b9c6-249">Decimal</span></span>
<span data-ttu-id="3b9c6-250">BOOLE DEĞERİ</span><span class="sxs-lookup"><span data-stu-id="3b9c6-250">BOOLEAN</span></span> | <span data-ttu-id="3b9c6-251">Bayt</span><span class="sxs-lookup"><span data-stu-id="3b9c6-251">Byte</span></span>
<span data-ttu-id="3b9c6-252">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="3b9c6-252">VARCHAR</span></span> | <span data-ttu-id="3b9c6-253">Dize</span><span class="sxs-lookup"><span data-stu-id="3b9c6-253">String</span></span>
<span data-ttu-id="3b9c6-254">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="3b9c6-254">NVARCHAR</span></span> | <span data-ttu-id="3b9c6-255">Dize</span><span class="sxs-lookup"><span data-stu-id="3b9c6-255">String</span></span>
<span data-ttu-id="3b9c6-256">CLOB</span><span class="sxs-lookup"><span data-stu-id="3b9c6-256">CLOB</span></span> | <span data-ttu-id="3b9c6-257">Byte]</span><span class="sxs-lookup"><span data-stu-id="3b9c6-257">Byte[]</span></span>
<span data-ttu-id="3b9c6-258">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="3b9c6-258">ALPHANUM</span></span> | <span data-ttu-id="3b9c6-259">Dize</span><span class="sxs-lookup"><span data-stu-id="3b9c6-259">String</span></span>
<span data-ttu-id="3b9c6-260">BLOB</span><span class="sxs-lookup"><span data-stu-id="3b9c6-260">BLOB</span></span> | <span data-ttu-id="3b9c6-261">Byte]</span><span class="sxs-lookup"><span data-stu-id="3b9c6-261">Byte[]</span></span>
<span data-ttu-id="3b9c6-262">TARİH</span><span class="sxs-lookup"><span data-stu-id="3b9c6-262">DATE</span></span> | <span data-ttu-id="3b9c6-263">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="3b9c6-263">DateTime</span></span>
<span data-ttu-id="3b9c6-264">SAAT</span><span class="sxs-lookup"><span data-stu-id="3b9c6-264">TIME</span></span> | <span data-ttu-id="3b9c6-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3b9c6-265">TimeSpan</span></span>
<span data-ttu-id="3b9c6-266">ZAMAN DAMGASI</span><span class="sxs-lookup"><span data-stu-id="3b9c6-266">TIMESTAMP</span></span> | <span data-ttu-id="3b9c6-267">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="3b9c6-267">DateTime</span></span>
<span data-ttu-id="3b9c6-268">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="3b9c6-268">SECONDDATE</span></span> | <span data-ttu-id="3b9c6-269">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="3b9c6-269">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="3b9c6-270">Bilinen sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="3b9c6-270">Known limitations</span></span>
<span data-ttu-id="3b9c6-271">SAP HANA veri kopyalama işlemi sırasında birkaç bilinen sınırlamalar vardır:</span><span class="sxs-lookup"><span data-stu-id="3b9c6-271">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="3b9c6-272">En fazla 4000 Unicode karakter uzunluğunu NVARCHAR dizeleri kesiliyor</span><span class="sxs-lookup"><span data-stu-id="3b9c6-272">NVARCHAR strings are truncated to maximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="3b9c6-273">SMALLDECIMAL desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="3b9c6-273">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="3b9c6-274">VARBINARY desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="3b9c6-274">VARBINARY is not supported</span></span>
- <span data-ttu-id="3b9c6-275">Geçerli bir tarih olan 12/1899/30 arasında ile 9999/12/31</span><span class="sxs-lookup"><span data-stu-id="3b9c6-275">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="3b9c6-276">Kaynak havuzu sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="3b9c6-276">Map source to sink columns</span></span>
<span data-ttu-id="3b9c6-277">Havuz dataset sütunlara kaynak kümesindeki eşleme sütunları hakkında bilgi edinmek için [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="3b9c6-277">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="3b9c6-278">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="3b9c6-278">Repeatable read from relational sources</span></span>
<span data-ttu-id="3b9c6-279">İlişkisel veri kopyalama verileri depoladığında, Yinelenebilirlik istenmeyen sonuçları önlemek için göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-279">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="3b9c6-280">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-280">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="3b9c6-281">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="3b9c6-282">Bir dilim iki yolla yeniden çalıştırıldığında, aynı veri dilimi çalıştırmak kaç kez geçtiğinden bağımsız okuduğunuzdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-282">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="3b9c6-283">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="3b9c6-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="3b9c6-284">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="3b9c6-284">Performance and Tuning</span></span>
<span data-ttu-id="3b9c6-285">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve onu en iyi duruma getirmek için çeşitli yollar etkisi performansını anahtar Etkenler hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="3b9c6-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
