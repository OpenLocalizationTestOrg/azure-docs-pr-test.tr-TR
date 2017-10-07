---
title: Azure Data Factory kullanarak SAP HANA aaaMove verilerden | Microsoft Docs
description: "Hakkında bilgi edinin Azure Data Factory kullanarak SAP HANA toomove verileri."
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
ms.openlocfilehash: 5cefe4c8ed01ea4e86e02496b2f8a9083d0b949c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="ca6bf-103">Veri gelen SAP, HANA Azure Data Factory kullanarak Taşı</span><span class="sxs-lookup"><span data-stu-id="ca6bf-103">Move data From SAP HANA using Azure Data Factory</span></span>
<span data-ttu-id="ca6bf-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove verileri bir şirket içi SAP HANA de açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP HANA.</span></span> <span data-ttu-id="ca6bf-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="ca6bf-106">Bir şirket içi SAP HANA veri deposu desteklenen tooany havuz veri deposundan verileri kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-106">You can copy data from an on-premises SAP HANA data store tooany supported sink data store.</span></span> <span data-ttu-id="ca6bf-107">Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="ca6bf-108">Veri Fabrikası şu anda destekleyen bir SAP HANA tooother verilerden veri depolar, ancak taşıma yalnızca verileri diğer veriler taşıma tooan SAP HANA depolar için.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-108">Data factory currently supports only moving data from an SAP HANA tooother data stores, but not for moving data from other data stores tooan SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="ca6bf-109">Desteklenen sürümleri ve yükleme</span><span class="sxs-lookup"><span data-stu-id="ca6bf-109">Supported versions and installation</span></span>
<span data-ttu-id="ca6bf-110">Bu bağlayıcı SAP HANA veritabanına herhangi bir sürümünü destekler.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-110">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="ca6bf-111">HANA bilgi modeli (gibi Analitik ve hesaplama görünümleri) ve SQL sorgularını kullanarak satır/sütun tablolarından veri kopyalamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="ca6bf-112">tooenable hello bağlantı toohello SAP HANA örneği bileşenleri aşağıdaki hello yükleyin:</span><span class="sxs-lookup"><span data-stu-id="ca6bf-112">tooenable hello connectivity toohello SAP HANA instance, install hello following components:</span></span>
- <span data-ttu-id="ca6bf-113">**Veri Yönetimi ağ geçidi**: Data Factory hizmeti destekler tooon içi verilere bağlanma (SAP HANA dahil) depoları bir bileşeni kullanılarak veri yönetimi ağ geçidi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="ca6bf-114">Veri Yönetimi ağ geçidi ve hello ağ geçidi, kurmak için adım adım yönergeler hakkında toolearn bkz [şirket içi veri arasında taşıma verilerini depolamak toocloud veri deposu](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="ca6bf-115">SAP HANA Hello bir Azure Iaas sanal makine (VM) barındırılan olsa bile ağ geçidi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-115">Gateway is required even if hello SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="ca6bf-116">Merhaba ağ geçidi üzerinde aynı VM hello veri olarak depolamak veya hello ağ geçidi olarak aynı uzunlukta farklı bir VM üzerinde toohello veritabanı bağlanabilir hello yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="ca6bf-117">**SAP HANA ODBC sürücüsü** hello gateway makinesinde.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-117">**SAP HANA ODBC driver** on hello gateway machine.</span></span> <span data-ttu-id="ca6bf-118">Hello hello SAP HANA ODBC sürücüsü indirebilirsiniz [SAP yazılım İndirme Merkezi](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="ca6bf-118">You can download hello SAP HANA ODBC driver from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="ca6bf-119">Arama hello anahtar sözcüğü ile **Windows için SAP HANA İSTEMCİSİ**.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-119">Search with hello keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="ca6bf-120">Başlarken</span><span class="sxs-lookup"><span data-stu-id="ca6bf-120">Getting started</span></span>
<span data-ttu-id="ca6bf-121">Farklı araçlar/API'lerini kullanarak bir şirket içi Cassandra veri deposundan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="ca6bf-122">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="ca6bf-123">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="ca6bf-124">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ca6bf-125">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="ca6bf-126">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ca6bf-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="ca6bf-127">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="ca6bf-128">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="ca6bf-129">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="ca6bf-130">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="ca6bf-131">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="ca6bf-132">Bir şirket içi SAP HANA kullanılan toocopy veri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: Blob SAP HANA tooAzure veri kopyalama](#json-example-copy-data-from-sap-hana-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA tooAzure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="ca6bf-133">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooan SAP HANA veri deposu olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="ca6bf-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="ca6bf-134">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="ca6bf-134">Linked service properties</span></span>
<span data-ttu-id="ca6bf-135">Aşağıdaki tablonun hello bağlantılı hizmetinin JSON öğeleri belirli tooSAP HANA açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-135">hello following table provides description for JSON elements specific tooSAP HANA linked service.</span></span>

<span data-ttu-id="ca6bf-136">Özellik</span><span class="sxs-lookup"><span data-stu-id="ca6bf-136">Property</span></span> | <span data-ttu-id="ca6bf-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ca6bf-137">Description</span></span> | <span data-ttu-id="ca6bf-138">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="ca6bf-138">Allowed values</span></span> | <span data-ttu-id="ca6bf-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ca6bf-139">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="ca6bf-140">sunucu</span><span class="sxs-lookup"><span data-stu-id="ca6bf-140">server</span></span> | <span data-ttu-id="ca6bf-141">Hangi hello SAP HANA örneği bulunduğu hello sunucusunun adı.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-141">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="ca6bf-142">Sunucunuz özelleştirilmiş bir bağlantı noktası kullanıyorsa belirtin `server:port`.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-142">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="ca6bf-143">Dize</span><span class="sxs-lookup"><span data-stu-id="ca6bf-143">string</span></span> | <span data-ttu-id="ca6bf-144">Evet</span><span class="sxs-lookup"><span data-stu-id="ca6bf-144">Yes</span></span>
<span data-ttu-id="ca6bf-145">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ca6bf-145">authenticationType</span></span> | <span data-ttu-id="ca6bf-146">Kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-146">Type of authentication.</span></span> | <span data-ttu-id="ca6bf-147">Dize.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-147">string.</span></span> <span data-ttu-id="ca6bf-148">"Temel" veya "Windows"</span><span class="sxs-lookup"><span data-stu-id="ca6bf-148">"Basic" or "Windows"</span></span> | <span data-ttu-id="ca6bf-149">Evet</span><span class="sxs-lookup"><span data-stu-id="ca6bf-149">Yes</span></span> 
<span data-ttu-id="ca6bf-150">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="ca6bf-150">username</span></span> | <span data-ttu-id="ca6bf-151">Erişim toohello SAP sunucusuna sahip hello kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="ca6bf-151">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="ca6bf-152">Dize</span><span class="sxs-lookup"><span data-stu-id="ca6bf-152">string</span></span> | <span data-ttu-id="ca6bf-153">Evet</span><span class="sxs-lookup"><span data-stu-id="ca6bf-153">Yes</span></span>
<span data-ttu-id="ca6bf-154">password</span><span class="sxs-lookup"><span data-stu-id="ca6bf-154">password</span></span> | <span data-ttu-id="ca6bf-155">Merhaba kullanıcının parolası.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-155">Password for hello user.</span></span> | <span data-ttu-id="ca6bf-156">Dize</span><span class="sxs-lookup"><span data-stu-id="ca6bf-156">string</span></span> | <span data-ttu-id="ca6bf-157">Evet</span><span class="sxs-lookup"><span data-stu-id="ca6bf-157">Yes</span></span>
<span data-ttu-id="ca6bf-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ca6bf-158">gatewayName</span></span> | <span data-ttu-id="ca6bf-159">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi SAP HANA örneğini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="ca6bf-160">Dize</span><span class="sxs-lookup"><span data-stu-id="ca6bf-160">string</span></span> | <span data-ttu-id="ca6bf-161">Evet</span><span class="sxs-lookup"><span data-stu-id="ca6bf-161">Yes</span></span>
<span data-ttu-id="ca6bf-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="ca6bf-162">encryptedCredential</span></span> | <span data-ttu-id="ca6bf-163">şifrelenmiş hello kimlik dizesi.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-163">hello encrypted credential string.</span></span> | <span data-ttu-id="ca6bf-164">Dize</span><span class="sxs-lookup"><span data-stu-id="ca6bf-164">string</span></span> | <span data-ttu-id="ca6bf-165">Hayır</span><span class="sxs-lookup"><span data-stu-id="ca6bf-165">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="ca6bf-166">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="ca6bf-166">Dataset properties</span></span>
<span data-ttu-id="ca6bf-167">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-167">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="ca6bf-168">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="ca6bf-169">Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-169">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="ca6bf-170">Merhaba SAP HANA dataset türü için desteklenen türüne özgü özellikler yok **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-170">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="ca6bf-171">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="ca6bf-171">Copy activity properties</span></span>
<span data-ttu-id="ca6bf-172">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-172">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ca6bf-173">Ad, açıklama, giriş ve çıkış tabloları gibi özellikleri olan ilkeleri etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="ca6bf-174">Oysa hello kullanılabilen özellikleri **typeProperties** hello etkinlik bölümünü her etkinlik türü ile değişir.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-174">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="ca6bf-175">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-175">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="ca6bf-176">Kopyalama etkinliği kaynağında türü olduğunda **RelationalSource** (içeren SAP HANA), aşağıdaki özelliklere hello typeProperties bölümünde bulunur:</span><span class="sxs-lookup"><span data-stu-id="ca6bf-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="ca6bf-177">Özellik</span><span class="sxs-lookup"><span data-stu-id="ca6bf-177">Property</span></span> | <span data-ttu-id="ca6bf-178">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ca6bf-178">Description</span></span> | <span data-ttu-id="ca6bf-179">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="ca6bf-179">Allowed values</span></span> | <span data-ttu-id="ca6bf-180">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ca6bf-180">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ca6bf-181">sorgu</span><span class="sxs-lookup"><span data-stu-id="ca6bf-181">query</span></span> | <span data-ttu-id="ca6bf-182">Merhaba SQL sorgu tooread veri hello SAP HANA örneğinden belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-182">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="ca6bf-183">SQL sorgusu.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-183">SQL query.</span></span> | <span data-ttu-id="ca6bf-184">Evet</span><span class="sxs-lookup"><span data-stu-id="ca6bf-184">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-tooazure-blob"></a><span data-ttu-id="ca6bf-185">JSON örnek: Blob SAP HANA tooAzure veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="ca6bf-185">JSON example: Copy data from SAP HANA tooAzure Blob</span></span>
<span data-ttu-id="ca6bf-186">Merhaba aşağıdaki örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ca6bf-186">hello following sample provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="ca6bf-187">Bu örnek göstermektedir nasıl bir şirket içi SAP HANA tooan Azure Blob Storage toocopy verileri.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-187">This sample shows how toocopy data from an on-premises SAP HANA tooan Azure Blob Storage.</span></span> <span data-ttu-id="ca6bf-188">Ancak, veriler kopyalanabilir **doğrudan** listelenen hello havuzlarını tooany [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-188">However, data can be copied **directly** tooany of hello sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="ca6bf-189">Bu örnek, JSON parçacıklarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-189">This sample provides JSON snippets.</span></span> <span data-ttu-id="ca6bf-190">Merhaba veri fabrikası oluşturma için yönergeler içermez.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-190">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="ca6bf-191">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="ca6bf-192">Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="ca6bf-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="ca6bf-193">Bağlı hizmet türü [SapHana](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ca6bf-193">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="ca6bf-194">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ca6bf-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ca6bf-195">Bir giriş [dataset](data-factory-create-datasets.md) türü [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ca6bf-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="ca6bf-196">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ca6bf-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="ca6bf-197">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ca6bf-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="ca6bf-198">Merhaba örnek verileri saatte bir SAP HANA örneği tooan Azure blob kopyalar.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-198">hello sample copies data from an SAP HANA instance tooan Azure blob hourly.</span></span> <span data-ttu-id="ca6bf-199">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="ca6bf-200">İlk adım olarak, hello veri yönetimi ağ geçidi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="ca6bf-201">Merhaba yönergelerdir hello [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="ca6bf-202">SAP HANA bağlı hizmet</span><span class="sxs-lookup"><span data-stu-id="ca6bf-202">SAP HANA linked service</span></span>
<span data-ttu-id="ca6bf-203">Bu hizmet bağlantıları SAP HANA örneği toohello data factory'nizi bağlı.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-203">This linked service links your SAP HANA instance toohello data factory.</span></span> <span data-ttu-id="ca6bf-204">Merhaba type özelliği çok ayarlamak**SapHana**.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-204">hello type property is set too**SapHana**.</span></span> <span data-ttu-id="ca6bf-205">Merhaba typeProperties bölüm hello SAP HANA örneği için bağlantı bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-205">hello typeProperties section provides connection information for hello SAP HANA instance.</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="ca6bf-206">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="ca6bf-206">Azure Storage linked service</span></span>
<span data-ttu-id="ca6bf-207">Bu hizmeti Azure Storage hesabı toohello data factory'nizi bağlı.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-207">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="ca6bf-208">Merhaba type özelliği çok ayarlamak**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-208">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="ca6bf-209">Merhaba typeProperties bölüm hello Azure depolama hesabı bağlantı bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-209">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="ca6bf-210">SAP HANA giriş veri kümesi</span><span class="sxs-lookup"><span data-stu-id="ca6bf-210">SAP HANA input dataset</span></span>

<span data-ttu-id="ca6bf-211">Bu veri kümesi hello SAP HANA veri kümesini tanımlamaktadır.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-211">This dataset defines hello SAP HANA dataset.</span></span> <span data-ttu-id="ca6bf-212">Merhaba Data Factory veri kümesi hello türü çok ayarlamak**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-212">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="ca6bf-213">Şu anda, SAP HANA veri kümesi için herhangi bir türe özgü özelliği belirtmeyin.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="ca6bf-214">Merhaba kopyalama etkinliği tanımı Hello sorguda hangi veri tooread hello SAP HANA örneğinden belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-214">hello query in hello Copy Activity definition specifies what data tooread from hello SAP HANA instance.</span></span> 

<span data-ttu-id="ca6bf-215">Dış özellik tootrue ayarı hello Data Factory hizmetinin bu hello tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil bildirir.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-215">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="ca6bf-216">Sıklık ve aralığı özelliklerini hello zamanlama tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-216">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="ca6bf-217">Bu durumda, hello veri hello SAP HANA örneğinden saatlik okunur.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-217">In this case, hello data is read from hello SAP HANA instance hourly.</span></span> 

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="ca6bf-218">Azure Blob çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="ca6bf-218">Azure Blob output dataset</span></span>
<span data-ttu-id="ca6bf-219">Bu veri kümesi hello çıktı Azure Blob dataset tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-219">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="ca6bf-220">Merhaba type özelliği tooAzureBlob ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-220">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="ca6bf-221">Merhaba typeProperties bölüm hello SAP HANA örneğinden kopyalanan hello verilerinin depolandığı sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-221">hello typeProperties section provides where hello data copied from hello SAP HANA instance is stored.</span></span> <span data-ttu-id="ca6bf-222">Merhaba veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="ca6bf-222">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ca6bf-223">hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-223">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="ca6bf-224">Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="ca6bf-225">Kopyalama etkinliği ile kanalı</span><span class="sxs-lookup"><span data-stu-id="ca6bf-225">Pipeline with Copy activity</span></span>

<span data-ttu-id="ca6bf-226">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="ca6bf-227">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**RelationalSource** (SAP HANA kaynağı için) ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP HANA source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="ca6bf-228">Merhaba belirtilen hello SQL sorgusu **sorgu** özelliği saat toocopy geçmiş hello hello veri seçer.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-228">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="ca6bf-229">SAP HANA türü eşlemesi</span><span class="sxs-lookup"><span data-stu-id="ca6bf-229">Type mapping for SAP HANA</span></span>
<span data-ttu-id="ca6bf-230">Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri iki aşamalı bir yaklaşım aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="ca6bf-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="ca6bf-231">Yerel kaynak türleri too.NET türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="ca6bf-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="ca6bf-232">.NET türü toonative havuz türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="ca6bf-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="ca6bf-233">SAP HANA verilerin taşınması, eşlemeleri aşağıdaki hello SAP HANA türleri too.NET türlerinden kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-233">When moving data from SAP HANA, hello following mappings are used from SAP HANA types too.NET types.</span></span>

<span data-ttu-id="ca6bf-234">SAP HANA türü</span><span class="sxs-lookup"><span data-stu-id="ca6bf-234">SAP HANA Type</span></span> | <span data-ttu-id="ca6bf-235">.NET türü temelinde</span><span class="sxs-lookup"><span data-stu-id="ca6bf-235">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="ca6bf-236">MİNİ TAMSAYI</span><span class="sxs-lookup"><span data-stu-id="ca6bf-236">TINYINT</span></span> | <span data-ttu-id="ca6bf-237">Bayt</span><span class="sxs-lookup"><span data-stu-id="ca6bf-237">Byte</span></span>
<span data-ttu-id="ca6bf-238">TAMSAYI</span><span class="sxs-lookup"><span data-stu-id="ca6bf-238">SMALLINT</span></span> | <span data-ttu-id="ca6bf-239">Int16</span><span class="sxs-lookup"><span data-stu-id="ca6bf-239">Int16</span></span>
<span data-ttu-id="ca6bf-240">INT</span><span class="sxs-lookup"><span data-stu-id="ca6bf-240">INT</span></span> | <span data-ttu-id="ca6bf-241">Int32</span><span class="sxs-lookup"><span data-stu-id="ca6bf-241">Int32</span></span>
<span data-ttu-id="ca6bf-242">BIGINT</span><span class="sxs-lookup"><span data-stu-id="ca6bf-242">BIGINT</span></span> | <span data-ttu-id="ca6bf-243">Int64</span><span class="sxs-lookup"><span data-stu-id="ca6bf-243">Int64</span></span>
<span data-ttu-id="ca6bf-244">GERÇEK</span><span class="sxs-lookup"><span data-stu-id="ca6bf-244">REAL</span></span> | <span data-ttu-id="ca6bf-245">Tek</span><span class="sxs-lookup"><span data-stu-id="ca6bf-245">Single</span></span>
<span data-ttu-id="ca6bf-246">ÇİFT</span><span class="sxs-lookup"><span data-stu-id="ca6bf-246">DOUBLE</span></span> | <span data-ttu-id="ca6bf-247">Tek</span><span class="sxs-lookup"><span data-stu-id="ca6bf-247">Single</span></span>
<span data-ttu-id="ca6bf-248">ONDALIK</span><span class="sxs-lookup"><span data-stu-id="ca6bf-248">DECIMAL</span></span> | <span data-ttu-id="ca6bf-249">Ondalık</span><span class="sxs-lookup"><span data-stu-id="ca6bf-249">Decimal</span></span>
<span data-ttu-id="ca6bf-250">BOOLE DEĞERİ</span><span class="sxs-lookup"><span data-stu-id="ca6bf-250">BOOLEAN</span></span> | <span data-ttu-id="ca6bf-251">Bayt</span><span class="sxs-lookup"><span data-stu-id="ca6bf-251">Byte</span></span>
<span data-ttu-id="ca6bf-252">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="ca6bf-252">VARCHAR</span></span> | <span data-ttu-id="ca6bf-253">Dize</span><span class="sxs-lookup"><span data-stu-id="ca6bf-253">String</span></span>
<span data-ttu-id="ca6bf-254">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="ca6bf-254">NVARCHAR</span></span> | <span data-ttu-id="ca6bf-255">Dize</span><span class="sxs-lookup"><span data-stu-id="ca6bf-255">String</span></span>
<span data-ttu-id="ca6bf-256">CLOB</span><span class="sxs-lookup"><span data-stu-id="ca6bf-256">CLOB</span></span> | <span data-ttu-id="ca6bf-257">Byte]</span><span class="sxs-lookup"><span data-stu-id="ca6bf-257">Byte[]</span></span>
<span data-ttu-id="ca6bf-258">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="ca6bf-258">ALPHANUM</span></span> | <span data-ttu-id="ca6bf-259">Dize</span><span class="sxs-lookup"><span data-stu-id="ca6bf-259">String</span></span>
<span data-ttu-id="ca6bf-260">BLOB</span><span class="sxs-lookup"><span data-stu-id="ca6bf-260">BLOB</span></span> | <span data-ttu-id="ca6bf-261">Byte]</span><span class="sxs-lookup"><span data-stu-id="ca6bf-261">Byte[]</span></span>
<span data-ttu-id="ca6bf-262">TARİH</span><span class="sxs-lookup"><span data-stu-id="ca6bf-262">DATE</span></span> | <span data-ttu-id="ca6bf-263">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="ca6bf-263">DateTime</span></span>
<span data-ttu-id="ca6bf-264">SAAT</span><span class="sxs-lookup"><span data-stu-id="ca6bf-264">TIME</span></span> | <span data-ttu-id="ca6bf-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="ca6bf-265">TimeSpan</span></span>
<span data-ttu-id="ca6bf-266">ZAMAN DAMGASI</span><span class="sxs-lookup"><span data-stu-id="ca6bf-266">TIMESTAMP</span></span> | <span data-ttu-id="ca6bf-267">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="ca6bf-267">DateTime</span></span>
<span data-ttu-id="ca6bf-268">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="ca6bf-268">SECONDDATE</span></span> | <span data-ttu-id="ca6bf-269">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="ca6bf-269">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="ca6bf-270">Bilinen sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="ca6bf-270">Known limitations</span></span>
<span data-ttu-id="ca6bf-271">SAP HANA veri kopyalama işlemi sırasında birkaç bilinen sınırlamalar vardır:</span><span class="sxs-lookup"><span data-stu-id="ca6bf-271">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="ca6bf-272">NVARCHAR dizeler kesilmiş toomaximum uzunluğu 4000 Unicode karakterler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ca6bf-272">NVARCHAR strings are truncated toomaximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="ca6bf-273">SMALLDECIMAL desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="ca6bf-273">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="ca6bf-274">VARBINARY desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="ca6bf-274">VARBINARY is not supported</span></span>
- <span data-ttu-id="ca6bf-275">Geçerli bir tarih olan 12/1899/30 arasında ile 9999/12/31</span><span class="sxs-lookup"><span data-stu-id="ca6bf-275">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="ca6bf-276">Kaynak toosink sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="ca6bf-276">Map source toosink columns</span></span>
<span data-ttu-id="ca6bf-277">Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="ca6bf-277">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="ca6bf-278">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="ca6bf-278">Repeatable read from relational sources</span></span>
<span data-ttu-id="ca6bf-279">İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-279">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="ca6bf-280">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-280">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="ca6bf-281">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="ca6bf-282">Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-282">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="ca6bf-283">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="ca6bf-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="ca6bf-284">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="ca6bf-284">Performance and Tuning</span></span>
<span data-ttu-id="ca6bf-285">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="ca6bf-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
