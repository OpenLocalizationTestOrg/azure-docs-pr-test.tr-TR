---
title: OData kaynaklardan aaaMove veri | Microsoft Docs
description: "Azure Data Factory kullanarak OData toomove verileri nasıl kaynakları hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: de28fa56-3204-4546-a4df-21a21de43ed7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 328efe4fd274fb3e54c1d2f209e4614c77c1ff37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="fed5b-103">Verileri Azure Data Factory kullanarak gelen bir OData kaynağı taşıma</span><span class="sxs-lookup"><span data-stu-id="fed5b-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="fed5b-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri bir OData kaynaktan açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fed5b-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an OData source.</span></span> <span data-ttu-id="fed5b-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="fed5b-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="fed5b-106">Bir OData kaynağı desteklenen tooany havuz veri deposundan verileri kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fed5b-106">You can copy data from an OData source tooany supported sink data store.</span></span> <span data-ttu-id="fed5b-107">Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="fed5b-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="fed5b-108">Veri Fabrikası şu anda destekleyen bir OData kaynak tooother verilerden veri depolar, ancak taşıma yalnızca verileri diğer veriler taşıma tooan OData kaynağı depolar için.</span><span class="sxs-lookup"><span data-stu-id="fed5b-108">Data factory currently supports only moving data from an OData source tooother data stores, but not for moving data from other data stores tooan OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="fed5b-109">Desteklenen sürümler ve kimlik doğrulama türleri</span><span class="sxs-lookup"><span data-stu-id="fed5b-109">Supported versions and authentication types</span></span>
<span data-ttu-id="fed5b-110">Bu OData bağlayıcısını destekleyen OData sürüm 3.0 ve 4.0 ve hem bulut OData verilerden ve şirket içi OData kaynaklarına kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fed5b-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="fed5b-111">İkinci Hello için tooinstall hello veri yönetimi ağ geçidi gerekir.</span><span class="sxs-lookup"><span data-stu-id="fed5b-111">For hello latter, you need tooinstall hello Data Management Gateway.</span></span> <span data-ttu-id="fed5b-112">Bkz: [şirket içi ve bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale veri yönetimi ağ geçidi hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="fed5b-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="fed5b-113">Kimlik doğrulama türleri desteklenir:</span><span class="sxs-lookup"><span data-stu-id="fed5b-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="fed5b-114">tooaccess **bulut** OData akışı, kullanabileceğiniz anonim, temel (kullanıcı adı ve parola) veya Azure Active Directory tabanlı OAuth kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="fed5b-114">tooaccess **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="fed5b-115">tooaccess **şirket içi** OData akışı, kullanabileceğiniz anonim, temel (kullanıcı adı ve parola) veya Windows kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="fed5b-115">tooaccess **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="fed5b-116">Başlarken</span><span class="sxs-lookup"><span data-stu-id="fed5b-116">Getting started</span></span>
<span data-ttu-id="fed5b-117">Farklı araçlar/API'lerini kullanarak bir OData kaynaktan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fed5b-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="fed5b-118">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="fed5b-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="fed5b-119">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="fed5b-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="fed5b-120">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="fed5b-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="fed5b-121">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="fed5b-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="fed5b-122">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="fed5b-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="fed5b-123">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="fed5b-123">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="fed5b-124">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="fed5b-124">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="fed5b-125">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="fed5b-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="fed5b-126">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fed5b-126">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="fed5b-127">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="fed5b-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="fed5b-128">Bir OData kaynaktan kullanılan toocopy verileri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: OData kaynak tooAzure Blob veri kopyalama](#json-example-copy-data-from-odata-source-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="fed5b-128">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an OData source, see [JSON example: Copy data from OData source tooAzure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="fed5b-129">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooOData kaynağı JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="fed5b-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooOData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="fed5b-130">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="fed5b-130">Linked Service properties</span></span>
<span data-ttu-id="fed5b-131">Aşağıdaki tablonun hello JSON öğeleri belirli tooOData bağlantılı hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="fed5b-131">hello following table provides description for JSON elements specific tooOData linked service.</span></span>

| <span data-ttu-id="fed5b-132">Özellik</span><span class="sxs-lookup"><span data-stu-id="fed5b-132">Property</span></span> | <span data-ttu-id="fed5b-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fed5b-133">Description</span></span> | <span data-ttu-id="fed5b-134">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fed5b-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fed5b-135">type</span><span class="sxs-lookup"><span data-stu-id="fed5b-135">type</span></span> |<span data-ttu-id="fed5b-136">Merhaba type özelliği ayarlanmalıdır: **OData**</span><span class="sxs-lookup"><span data-stu-id="fed5b-136">hello type property must be set to: **OData**</span></span> |<span data-ttu-id="fed5b-137">Evet</span><span class="sxs-lookup"><span data-stu-id="fed5b-137">Yes</span></span> |
| <span data-ttu-id="fed5b-138">URL</span><span class="sxs-lookup"><span data-stu-id="fed5b-138">url</span></span> |<span data-ttu-id="fed5b-139">Merhaba OData hizmeti URL'si.</span><span class="sxs-lookup"><span data-stu-id="fed5b-139">Url of hello OData service.</span></span> |<span data-ttu-id="fed5b-140">Evet</span><span class="sxs-lookup"><span data-stu-id="fed5b-140">Yes</span></span> |
| <span data-ttu-id="fed5b-141">authenticationType</span><span class="sxs-lookup"><span data-stu-id="fed5b-141">authenticationType</span></span> |<span data-ttu-id="fed5b-142">Kimlik doğrulama türü tooconnect toohello OData kaynağı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fed5b-142">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="fed5b-143">OData bulut için olası değerler şunlardır anonim, temel ve OAuth (Not OAuth Azure Active Directory tabanlı şu anda yalnızca Azure Data Factory destek).</span><span class="sxs-lookup"><span data-stu-id="fed5b-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="fed5b-144">Anonim, temel ve Windows, şirket içi OData için olası değerler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="fed5b-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="fed5b-145">Evet</span><span class="sxs-lookup"><span data-stu-id="fed5b-145">Yes</span></span> |
| <span data-ttu-id="fed5b-146">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="fed5b-146">username</span></span> |<span data-ttu-id="fed5b-147">Temel kimlik doğrulamasını kullanıyorsanız kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="fed5b-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="fed5b-148">Evet (yalnızca temel kimlik doğrulaması kullanıyorsanız)</span><span class="sxs-lookup"><span data-stu-id="fed5b-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="fed5b-149">password</span><span class="sxs-lookup"><span data-stu-id="fed5b-149">password</span></span> |<span data-ttu-id="fed5b-150">Merhaba username için belirtilen hello kullanıcı hesabı için parola belirtin.</span><span class="sxs-lookup"><span data-stu-id="fed5b-150">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="fed5b-151">Evet (yalnızca temel kimlik doğrulaması kullanıyorsanız)</span><span class="sxs-lookup"><span data-stu-id="fed5b-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="fed5b-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="fed5b-152">authorizedCredential</span></span> |<span data-ttu-id="fed5b-153">OAuth kullanıyorsanız **Authorize** hello Data Factory Kopyalama Sihirbazı veya Düzenleyicisi'nde düğmesine tıklayın ve sonra bu özellik başlangıç değeri otomatik olarak oluşturulan kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="fed5b-153">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="fed5b-154">Evet (yalnızca OAuth kimlik doğrulaması kullanıyorsanız)</span><span class="sxs-lookup"><span data-stu-id="fed5b-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="fed5b-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="fed5b-155">gatewayName</span></span> |<span data-ttu-id="fed5b-156">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello şirket içi OData hizmeti kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fed5b-156">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="fed5b-157">Yalnızca şirket içi OData kaynak sunucudan kopyaladığınız verileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="fed5b-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="fed5b-158">Hayır</span><span class="sxs-lookup"><span data-stu-id="fed5b-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="fed5b-159">Temel kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="fed5b-159">Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="fed5b-160">Anonim kimlik doğrulamasını kullanma</span><span class="sxs-lookup"><span data-stu-id="fed5b-160">Using Anonymous authentication</span></span>
```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
        "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="fed5b-161">Şirket içi OData kaynağına erişme Windows kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="fed5b-161">Using Windows authentication accessing on-premises OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of on-premises OData source e.g. Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="fed5b-162">OAuth kimlik doğrulaması erişen bulut OData kaynağı kullanma</span><span class="sxs-lookup"><span data-stu-id="fed5b-162">Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source e.g. https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="fed5b-163">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="fed5b-163">Dataset properties</span></span>
<span data-ttu-id="fed5b-164">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="fed5b-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="fed5b-165">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="fed5b-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="fed5b-166">Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="fed5b-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="fed5b-167">Merhaba typeProperties bölüm türü veri kümesi için **ODataResource** hello aşağıdaki özelliklere sahip (OData veri kümesi içerir)</span><span class="sxs-lookup"><span data-stu-id="fed5b-167">hello typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has hello following properties</span></span>

| <span data-ttu-id="fed5b-168">Özellik</span><span class="sxs-lookup"><span data-stu-id="fed5b-168">Property</span></span> | <span data-ttu-id="fed5b-169">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fed5b-169">Description</span></span> | <span data-ttu-id="fed5b-170">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fed5b-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fed5b-171">Yol</span><span class="sxs-lookup"><span data-stu-id="fed5b-171">path</span></span> |<span data-ttu-id="fed5b-172">Yol toohello OData kaynak</span><span class="sxs-lookup"><span data-stu-id="fed5b-172">Path toohello OData resource</span></span> |<span data-ttu-id="fed5b-173">Hayır</span><span class="sxs-lookup"><span data-stu-id="fed5b-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="fed5b-174">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="fed5b-174">Copy activity properties</span></span>
<span data-ttu-id="fed5b-175">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="fed5b-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="fed5b-176">Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fed5b-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="fed5b-177">Özellikler hello hello faaliyete hello typeProperties bölümünde kullanılabilir diğer yandan farklılık ile her etkinlik türü.</span><span class="sxs-lookup"><span data-stu-id="fed5b-177">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="fed5b-178">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="fed5b-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="fed5b-179">Kaynak türü olduğunda **RelationalSource** (OData içerir) aşağıdaki özelliklere hello typeProperties bölümünde bulunur:</span><span class="sxs-lookup"><span data-stu-id="fed5b-179">When source is of type **RelationalSource** (which includes OData) hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="fed5b-180">Özellik</span><span class="sxs-lookup"><span data-stu-id="fed5b-180">Property</span></span> | <span data-ttu-id="fed5b-181">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fed5b-181">Description</span></span> | <span data-ttu-id="fed5b-182">Örnek</span><span class="sxs-lookup"><span data-stu-id="fed5b-182">Example</span></span> | <span data-ttu-id="fed5b-183">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fed5b-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fed5b-184">sorgu</span><span class="sxs-lookup"><span data-stu-id="fed5b-184">query</span></span> |<span data-ttu-id="fed5b-185">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="fed5b-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="fed5b-186">"? $select adı, açıklama ve $top = 5 ="</span><span class="sxs-lookup"><span data-stu-id="fed5b-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="fed5b-187">Hayır</span><span class="sxs-lookup"><span data-stu-id="fed5b-187">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="fed5b-188">Tür eşlemesi için OData</span><span class="sxs-lookup"><span data-stu-id="fed5b-188">Type Mapping for OData</span></span>
<span data-ttu-id="fed5b-189">Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri iki aşamalı bir yaklaşım aşağıdaki hello ile.</span><span class="sxs-lookup"><span data-stu-id="fed5b-189">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="fed5b-190">Yerel kaynak türleri too.NET türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="fed5b-190">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="fed5b-191">.NET türü toonative havuz türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="fed5b-191">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="fed5b-192">Veri OData taşırken hello aşağıdaki eşlemelerini OData türlerini too.NET türünden kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fed5b-192">When moving data from OData, hello following mappings are used from OData types too.NET type.</span></span>

| <span data-ttu-id="fed5b-193">OData veri türü</span><span class="sxs-lookup"><span data-stu-id="fed5b-193">OData Data Type</span></span> | <span data-ttu-id="fed5b-194">.NET türü</span><span class="sxs-lookup"><span data-stu-id="fed5b-194">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="fed5b-195">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="fed5b-195">Edm.Binary</span></span> |<span data-ttu-id="fed5b-196">Byte]</span><span class="sxs-lookup"><span data-stu-id="fed5b-196">Byte[]</span></span> |
| <span data-ttu-id="fed5b-197">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="fed5b-197">Edm.Boolean</span></span> |<span data-ttu-id="fed5b-198">bool</span><span class="sxs-lookup"><span data-stu-id="fed5b-198">Bool</span></span> |
| <span data-ttu-id="fed5b-199">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="fed5b-199">Edm.Byte</span></span> |<span data-ttu-id="fed5b-200">Byte]</span><span class="sxs-lookup"><span data-stu-id="fed5b-200">Byte[]</span></span> |
| <span data-ttu-id="fed5b-201">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="fed5b-201">Edm.DateTime</span></span> |<span data-ttu-id="fed5b-202">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="fed5b-202">DateTime</span></span> |
| <span data-ttu-id="fed5b-203">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="fed5b-203">Edm.Decimal</span></span> |<span data-ttu-id="fed5b-204">Ondalık</span><span class="sxs-lookup"><span data-stu-id="fed5b-204">Decimal</span></span> |
| <span data-ttu-id="fed5b-205">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="fed5b-205">Edm.Double</span></span> |<span data-ttu-id="fed5b-206">Çift</span><span class="sxs-lookup"><span data-stu-id="fed5b-206">Double</span></span> |
| <span data-ttu-id="fed5b-207">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="fed5b-207">Edm.Single</span></span> |<span data-ttu-id="fed5b-208">Tek</span><span class="sxs-lookup"><span data-stu-id="fed5b-208">Single</span></span> |
| <span data-ttu-id="fed5b-209">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="fed5b-209">Edm.Guid</span></span> |<span data-ttu-id="fed5b-210">GUID</span><span class="sxs-lookup"><span data-stu-id="fed5b-210">Guid</span></span> |
| <span data-ttu-id="fed5b-211">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="fed5b-211">Edm.Int16</span></span> |<span data-ttu-id="fed5b-212">Int16</span><span class="sxs-lookup"><span data-stu-id="fed5b-212">Int16</span></span> |
| <span data-ttu-id="fed5b-213">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="fed5b-213">Edm.Int32</span></span> |<span data-ttu-id="fed5b-214">Int32</span><span class="sxs-lookup"><span data-stu-id="fed5b-214">Int32</span></span> |
| <span data-ttu-id="fed5b-215">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="fed5b-215">Edm.Int64</span></span> |<span data-ttu-id="fed5b-216">Int64</span><span class="sxs-lookup"><span data-stu-id="fed5b-216">Int64</span></span> |
| <span data-ttu-id="fed5b-217">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="fed5b-217">Edm.SByte</span></span> |<span data-ttu-id="fed5b-218">Int16</span><span class="sxs-lookup"><span data-stu-id="fed5b-218">Int16</span></span> |
| <span data-ttu-id="fed5b-219">Edm.String</span><span class="sxs-lookup"><span data-stu-id="fed5b-219">Edm.String</span></span> |<span data-ttu-id="fed5b-220">Dize</span><span class="sxs-lookup"><span data-stu-id="fed5b-220">String</span></span> |
| <span data-ttu-id="fed5b-221">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="fed5b-221">Edm.Time</span></span> |<span data-ttu-id="fed5b-222">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="fed5b-222">TimeSpan</span></span> |
| <span data-ttu-id="fed5b-223">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="fed5b-223">Edm.DateTimeOffset</span></span> |<span data-ttu-id="fed5b-224">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="fed5b-224">DateTimeOffset</span></span> |

> [!Note]
> <span data-ttu-id="fed5b-225">OData karmaşık veri türleri örneğin nesnesi desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="fed5b-225">OData complex data types e.g. Object are not supported.</span></span>

## <a name="json-example-copy-data-from-odata-source-tooazure-blob"></a><span data-ttu-id="fed5b-226">JSON örnek: OData kaynak tooAzure Blob veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="fed5b-226">JSON example: Copy data from OData source tooAzure Blob</span></span>
<span data-ttu-id="fed5b-227">Bu örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fed5b-227">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="fed5b-228">Bunlar, nasıl bir OData toocopy verileri tooan Azure Blob Depolama kaynağı gösterir.</span><span class="sxs-lookup"><span data-stu-id="fed5b-228">They show how toocopy data from an OData source tooan Azure Blob Storage.</span></span> <span data-ttu-id="fed5b-229">Ancak, veri belirtildiği hello havuzlarını, kopyalanan tooany olabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="fed5b-229">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="fed5b-230">Merhaba örnek Data Factory varlıklarını aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="fed5b-230">hello sample has hello following Data Factory entities:</span></span>

1. <span data-ttu-id="fed5b-231">Bağlı hizmet türü [OData](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fed5b-231">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="fed5b-232">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fed5b-232">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="fed5b-233">Bir giriş [dataset](data-factory-create-datasets.md) türü [ODataResource](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fed5b-233">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="fed5b-234">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fed5b-234">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="fed5b-235">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="fed5b-235">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="fed5b-236">Merhaba örnek verileri bir OData kaynak tooan karşı Azure blob saatte sorgulamasını kopyalar.</span><span class="sxs-lookup"><span data-stu-id="fed5b-236">hello sample copies data from querying against an OData source tooan Azure blob every hour.</span></span> <span data-ttu-id="fed5b-237">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="fed5b-237">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="fed5b-238">**OData bağlantılı hizmeti:** kullandığı hello anonim kimlik doğrulaması Bu örnek.</span><span class="sxs-lookup"><span data-stu-id="fed5b-238">**OData linked service:** This example uses hello Anonymous authentication.</span></span> <span data-ttu-id="fed5b-239">Bkz: [OData bağlantılı hizmeti](#linked-service-properties) bölümü için farklı tür kimlik doğrulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fed5b-239">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
            }
        }
}
```

<span data-ttu-id="fed5b-240">**Azure Storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="fed5b-240">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="fed5b-241">**OData giriş veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="fed5b-241">**OData input dataset:**</span></span>

<span data-ttu-id="fed5b-242">"Dış" ayarı: "true" bildirir hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="fed5b-242">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "ODataDataset",
    "properties":
    {
        "type": "ODataResource",
        "typeProperties":
        {
                "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3                
        }
    }
}
```

<span data-ttu-id="fed5b-243">Belirtme **yolu** hello kümesinde tanımı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="fed5b-243">Specifying **path** in hello dataset definition is optional.</span></span>

<span data-ttu-id="fed5b-244">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="fed5b-244">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="fed5b-245">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="fed5b-245">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="fed5b-246">hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="fed5b-246">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="fed5b-247">Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="fed5b-247">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobODataDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


<span data-ttu-id="fed5b-248">**OData kaynağı ve Blob havuz ile ardışık düzeninde etkinlik kopyalayın:**</span><span class="sxs-lookup"><span data-stu-id="fed5b-248">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="fed5b-249">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="fed5b-249">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="fed5b-250">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**RelationalSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="fed5b-250">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="fed5b-251">Merhaba belirtilen hello SQL sorgusu **sorgu** özelliği hello OData kaynağından hello en son (yeni) verileri seçer.</span><span class="sxs-lookup"><span data-stu-id="fed5b-251">hello SQL query specified for hello **query** property selects hello latest (newest) data from hello OData source.</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "?$select=Name, Description&$top=5",
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "ODataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobODataDataSet"
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
                "name": "ODataToBlob"
            }
        ],
        "start": "2017-02-01T18:00:00Z",
        "end": "2017-02-03T19:00:00Z"
    }
}
```

<span data-ttu-id="fed5b-252">Belirtme **sorgu** hello ardışık düzeninde tanımı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="fed5b-252">Specifying **query** in hello pipeline definition is optional.</span></span> <span data-ttu-id="fed5b-253">Merhaba **URL** hello Data Factory hizmetinin tooretrieve veri kullanır: Merhaba bağlantılı hizmeti (gerekli) + (isteğe bağlı) hello dataset belirtilen yolu + sorgu (isteğe bağlı) hello ardışık düzeninde URL belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="fed5b-253">hello **URL** that hello Data Factory service uses tooretrieve data is: URL specified in hello linked service (required) + path specified in hello dataset (optional) + query in hello pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="fed5b-254">Tür eşlemesi için OData</span><span class="sxs-lookup"><span data-stu-id="fed5b-254">Type mapping for OData</span></span>
<span data-ttu-id="fed5b-255">Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği gerçekleştiren kaynak türleri toosink türlerinden otomatik tür dönüşümleri 2 adımlı yaklaşımı izleyerek hello ile:</span><span class="sxs-lookup"><span data-stu-id="fed5b-255">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="fed5b-256">Yerel kaynak türleri too.NET türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="fed5b-256">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="fed5b-257">.NET türü toonative havuz türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="fed5b-257">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="fed5b-258">OData veri depolarına verilerin taşınması, OData veri türleri eşlenen too.NET türleridir.</span><span class="sxs-lookup"><span data-stu-id="fed5b-258">When moving data from OData data stores, OData data types are mapped too.NET types.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="fed5b-259">Kaynak toosink sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="fed5b-259">Map source toosink columns</span></span>
<span data-ttu-id="fed5b-260">Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="fed5b-260">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="fed5b-261">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="fed5b-261">Repeatable read from relational sources</span></span>
<span data-ttu-id="fed5b-262">İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları.</span><span class="sxs-lookup"><span data-stu-id="fed5b-262">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="fed5b-263">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fed5b-263">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="fed5b-264">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fed5b-264">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="fed5b-265">Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fed5b-265">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="fed5b-266">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="fed5b-266">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="fed5b-267">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="fed5b-267">Performance and Tuning</span></span>
<span data-ttu-id="fed5b-268">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="fed5b-268">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
