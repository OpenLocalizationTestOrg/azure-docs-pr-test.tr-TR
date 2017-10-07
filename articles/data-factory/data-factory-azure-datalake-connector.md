---
title: Azure Data Lake Store gelen aaaCopy veri tooand | Microsoft Docs
description: "Bilgi nasıl Azure Data Factory kullanarak Data Lake Store gelen toocopy veri tooand"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a><span data-ttu-id="93cdf-103">Veri Fabrikası kullanarak veri tooand Data Lake Deposu'ndan veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="93cdf-103">Copy data tooand from Data Lake Store by using Data Factory</span></span>
<span data-ttu-id="93cdf-104">Bu makalede açıklanır nasıl toouse kopya etkinliği Azure Data Factory toomove veri tooand Azure Data Lake Store gelen içinde.</span><span class="sxs-lookup"><span data-stu-id="93cdf-104">This article explains how toouse Copy Activity in Azure Data Factory toomove data tooand from Azure Data Lake Store.</span></span> <span data-ttu-id="93cdf-105">Merhaba üzerinde derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalesi, veri taşıma kopyalama etkinliği ile bir genel bakış.</span><span class="sxs-lookup"><span data-stu-id="93cdf-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="93cdf-106">Desteklenen senaryolar</span><span class="sxs-lookup"><span data-stu-id="93cdf-106">Supported scenarios</span></span>
<span data-ttu-id="93cdf-107">Veri kopyalama **Azure Data Lake Store gelen** veri depolarına aşağıdaki toohello:</span><span class="sxs-lookup"><span data-stu-id="93cdf-107">You can copy data **from Azure Data Lake Store** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="93cdf-108">Veri depoları aşağıdaki hello verileri kopyalayabilirsiniz **tooAzure Data Lake Store**:</span><span class="sxs-lookup"><span data-stu-id="93cdf-108">You can copy data from hello following data stores **tooAzure Data Lake Store**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="93cdf-109">Kopyalama etkinliği ile işlem hattı oluşturmadan önce bir Data Lake Store hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="93cdf-109">Create a Data Lake Store account before creating a pipeline with Copy Activity.</span></span> <span data-ttu-id="93cdf-110">Daha fazla bilgi için bkz: [Azure Data Lake Store ile çalışmaya başlama](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="93cdf-110">For more information, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="93cdf-111">Desteklenen kimlik doğrulama türleri</span><span class="sxs-lookup"><span data-stu-id="93cdf-111">Supported authentication types</span></span>
<span data-ttu-id="93cdf-112">Merhaba Data Lake Store bağlayıcı, bu kimlik doğrulama türlerini destekler:</span><span class="sxs-lookup"><span data-stu-id="93cdf-112">hello Data Lake Store connector supports these authentication types:</span></span>
* <span data-ttu-id="93cdf-113">Hizmet sorumlusu kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="93cdf-113">Service principal authentication</span></span>
* <span data-ttu-id="93cdf-114">Kullanıcı kimlik bilgisi (OAuth) kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="93cdf-114">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="93cdf-115">Hizmet asıl kimlik doğrulaması, özellikle bir zamanlanmış veri kopyalama için kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="93cdf-115">We recommend that you use service principal authentication, especially for a scheduled data copy.</span></span> <span data-ttu-id="93cdf-116">Belirteç süre sonu davranış kullanıcı kimlik bilgilerinin ile ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="93cdf-116">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="93cdf-117">Merhaba yapılandırma ayrıntıları için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="93cdf-117">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>

## <a name="get-started"></a><span data-ttu-id="93cdf-118">başlarken</span><span class="sxs-lookup"><span data-stu-id="93cdf-118">Get started</span></span>
<span data-ttu-id="93cdf-119">Verileri farklı araçlar/API'lerini kullanarak Azure Data Lake Store denetleyicisinden taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="93cdf-119">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="93cdf-120">Merhaba en kolay yolu toocreate bir ardışık düzen toocopy veri olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="93cdf-120">hello easiest way toocreate a pipeline toocopy data is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="93cdf-121">Merhaba Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma, Öğretici için bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="93cdf-121">For a tutorial on creating a pipeline by using hello Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="93cdf-122">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="93cdf-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="93cdf-123">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="93cdf-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="93cdf-124">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="93cdf-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="93cdf-125">Oluşturma bir **veri fabrikası**.</span><span class="sxs-lookup"><span data-stu-id="93cdf-125">Create a **data factory**.</span></span> <span data-ttu-id="93cdf-126">Veri Fabrikası bir veya daha fazla ardışık düzen içerebilir.</span><span class="sxs-lookup"><span data-stu-id="93cdf-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="93cdf-127">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="93cdf-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="93cdf-128">Bir Azure blob depolama tooan Azure Data Lake Store veri kopyalama, örneğin, iki bağlı hizmet toolink Azure depolama hesabınız ve Azure Data Lake deposu tooyour veri fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="93cdf-128">For example, if you are copying data from an Azure blob storage tooan Azure Data Lake Store, you create two linked services toolink your Azure storage account and Azure Data Lake store tooyour data factory.</span></span> <span data-ttu-id="93cdf-129">Belirli tooAzure Data Lake Store bağlantılı hizmet özellikler için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="93cdf-129">For linked service properties that are specific tooAzure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="93cdf-130">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="93cdf-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="93cdf-131">Merhaba son adımda bahsedilen hello örnekte, bir veri kümesi toospecify hello blob kapsayıcısı ve hello giriş verisi içeren klasörü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="93cdf-131">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="93cdf-132">Ve hello blob depolama biriminden kopyalanan hello verilerini tutan hello Data Lake deposu başka bir veri kümesi toospecify hello klasör ve dosya yolu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="93cdf-132">And, you create another dataset toospecify hello folder and file path in hello Data Lake store that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="93cdf-133">Belirli tooAzure Data Lake Store dataset özellikler için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="93cdf-133">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="93cdf-134">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="93cdf-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="93cdf-135">Daha önce bahsedilen hello örnekte BlobSource bir kaynak ve AzureDataLakeStoreSink havuzu olarak hello kopya etkinliği için kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="93cdf-135">In hello example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for hello copy activity.</span></span> <span data-ttu-id="93cdf-136">Azure Data Lake Store tooAzure Blob Depolama kopyalıyorsanız benzer şekilde, AzureDataLakeStoreSource ve BlobSink hello kopyalama etkinliği kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="93cdf-136">Similarly, if you are copying from Azure Data Lake Store tooAzure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in hello copy activity.</span></span> <span data-ttu-id="93cdf-137">Belirli tooAzure Data Lake Store kopyalama etkinliği özellikler için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="93cdf-137">For copy activity properties that are specific tooAzure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="93cdf-138">Nasıl toouse bir veri deposu bir kaynak veya bir havuz olarak hakkında daha fazla bilgi için veri deposu hello önceki bölümdeki hello bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="93cdf-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="93cdf-139">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="93cdf-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="93cdf-140">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="93cdf-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="93cdf-141">Bir Azure Data Lake Store/kullanılan toocopy verileri olan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples-for-copying-data-to-and-from-data-lake-store) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="93cdf-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span></span>

<span data-ttu-id="93cdf-142">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooData Lake deposu JSON özellikleri hakkında ayrıntılı bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="93cdf-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooData Lake Store.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="93cdf-143">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="93cdf-143">Linked service properties</span></span>
<span data-ttu-id="93cdf-144">Bağlı hizmet, bir veri deposu tooa veri fabrikası bağlar.</span><span class="sxs-lookup"><span data-stu-id="93cdf-144">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="93cdf-145">Bağlı hizmet türü oluşturma **AzureDataLakeStore** toolink Data Lake Store veri tooyour data factory'nizi.</span><span class="sxs-lookup"><span data-stu-id="93cdf-145">You create a linked service of type **AzureDataLakeStore** toolink your Data Lake Store data tooyour data factory.</span></span> <span data-ttu-id="93cdf-146">Aşağıdaki tablonun hello JSON öğeleri belirli tooData Lake deposu bağlı Hizmetleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="93cdf-146">hello following table describes JSON elements specific tooData Lake Store linked services.</span></span> <span data-ttu-id="93cdf-147">Hizmet sorumlusu ve kullanıcı kimlik bilgileri doğrulaması arasında seçim yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93cdf-147">You can choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="93cdf-148">Özellik</span><span class="sxs-lookup"><span data-stu-id="93cdf-148">Property</span></span> | <span data-ttu-id="93cdf-149">Açıklama</span><span class="sxs-lookup"><span data-stu-id="93cdf-149">Description</span></span> | <span data-ttu-id="93cdf-150">Gerekli</span><span class="sxs-lookup"><span data-stu-id="93cdf-150">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="93cdf-151">**türü**</span><span class="sxs-lookup"><span data-stu-id="93cdf-151">**type**</span></span> | <span data-ttu-id="93cdf-152">Merhaba type özelliği çok ayarlanmalıdır**AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="93cdf-152">hello type property must be set too**AzureDataLakeStore**.</span></span> | <span data-ttu-id="93cdf-153">Evet</span><span class="sxs-lookup"><span data-stu-id="93cdf-153">Yes</span></span> |
| <span data-ttu-id="93cdf-154">**dataLakeStoreUri**</span><span class="sxs-lookup"><span data-stu-id="93cdf-154">**dataLakeStoreUri**</span></span> | <span data-ttu-id="93cdf-155">Hello Azure Data Lake Store hesabı hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="93cdf-155">Information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="93cdf-156">Bu bilgiler biçimleri aşağıdaki hello birini alır: `https://[accountname].azuredatalakestore.net/webhdfs/v1` veya `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="93cdf-156">This information takes one of hello following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="93cdf-157">Evet</span><span class="sxs-lookup"><span data-stu-id="93cdf-157">Yes</span></span> |
| <span data-ttu-id="93cdf-158">**Subscriptionıd**</span><span class="sxs-lookup"><span data-stu-id="93cdf-158">**subscriptionId**</span></span> | <span data-ttu-id="93cdf-159">Azure abonelik kimliği toowhich hello Data Lake Store hesabına ait.</span><span class="sxs-lookup"><span data-stu-id="93cdf-159">Azure subscription ID toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="93cdf-160">Havuz için gerekli</span><span class="sxs-lookup"><span data-stu-id="93cdf-160">Required for sink</span></span> |
| <span data-ttu-id="93cdf-161">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="93cdf-161">**resourceGroupName**</span></span> | <span data-ttu-id="93cdf-162">Azure kaynak grubu adı toowhich hello Data Lake Store hesabına ait.</span><span class="sxs-lookup"><span data-stu-id="93cdf-162">Azure resource group name toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="93cdf-163">Havuz için gerekli</span><span class="sxs-lookup"><span data-stu-id="93cdf-163">Required for sink</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="93cdf-164">(Önerilen) hizmet asıl kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="93cdf-164">Service principal authentication (recommended)</span></span>
<span data-ttu-id="93cdf-165">Kayıt, hello Azure Active Directory (Azure AD) ve grant uygulama varlık toouse hizmet asıl kimlik doğrulaması, tooData Lake Store erişin.</span><span class="sxs-lookup"><span data-stu-id="93cdf-165">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="93cdf-166">Ayrıntılı adımlar için bkz: [hizmeti için kimlik doğrulama](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="93cdf-166">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="93cdf-167">Kullandığınız değerler aşağıdaki hello Not toodefine hello bağlantılı hizmeti:</span><span class="sxs-lookup"><span data-stu-id="93cdf-167">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="93cdf-168">Uygulama Kimliği</span><span class="sxs-lookup"><span data-stu-id="93cdf-168">Application ID</span></span>
* <span data-ttu-id="93cdf-169">Uygulama anahtarı</span><span class="sxs-lookup"><span data-stu-id="93cdf-169">Application key</span></span> 
* <span data-ttu-id="93cdf-170">Kiracı Kimliği</span><span class="sxs-lookup"><span data-stu-id="93cdf-170">Tenant ID</span></span>

> [!IMPORTANT]
> <span data-ttu-id="93cdf-171">Merhaba Kopyalama Sihirbazı'nı tooauthor veri ardışık kullanıyorsanız, hello hizmet sorumlusu vermek emin olun. en az bir **okuyucu** hello Data Lake Store hesabı için erişim denetimi (kimlik ve erişim yönetimi) rolü.</span><span class="sxs-lookup"><span data-stu-id="93cdf-171">If you are using hello Copy Wizard tooauthor data pipelines, make sure that you grant hello service principal at least a **Reader** role in access control (identity and access management) for hello Data Lake Store account.</span></span> <span data-ttu-id="93cdf-172">Ayrıca, hello hizmet asıl en az izni **okuma + yürütme** izin tooyour Data Lake Store kök ("/") ve alt öğelerini.</span><span class="sxs-lookup"><span data-stu-id="93cdf-172">Also, grant hello service principal at least **Read + Execute** permission tooyour Data Lake Store root ("/") and its children.</span></span> <span data-ttu-id="93cdf-173">Aksi takdirde, selamlama iletisine "hello girilen kimlik bilgileri geçersiz." görebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="93cdf-173">Otherwise you might see hello message "hello credentials provided are invalid."</span></span><br/><br/>
<span data-ttu-id="93cdf-174">Oluşturma veya Azure AD içinde bir hizmet sorumlusu güncelleştirdikten sonra hello değişiklikleri tootake etkisi birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="93cdf-174">After you create or update a service principal in Azure AD, it can take a few minutes for hello changes tootake effect.</span></span> <span data-ttu-id="93cdf-175">Merhaba hizmet sorumlusu ve Data Lake Store erişim denetimi listesi (ACL) yapılandırmalarını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="93cdf-175">Check hello service principal and Data Lake Store access control list (ACL) configurations.</span></span> <span data-ttu-id="93cdf-176">Hala selamlama iletisine "geçersiz kimlik bilgileri sağlanan hello" görürseniz, bir süre bekleyin ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="93cdf-176">If you still see hello message "hello credentials provided are invalid," wait a while and try again.</span></span>

<span data-ttu-id="93cdf-177">Aşağıdaki özelliklere hello belirterek hizmet asıl kimlik doğrulamasını kullan:</span><span class="sxs-lookup"><span data-stu-id="93cdf-177">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="93cdf-178">Özellik</span><span class="sxs-lookup"><span data-stu-id="93cdf-178">Property</span></span> | <span data-ttu-id="93cdf-179">Açıklama</span><span class="sxs-lookup"><span data-stu-id="93cdf-179">Description</span></span> | <span data-ttu-id="93cdf-180">Gerekli</span><span class="sxs-lookup"><span data-stu-id="93cdf-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="93cdf-181">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="93cdf-181">**servicePrincipalId**</span></span> | <span data-ttu-id="93cdf-182">Merhaba uygulamanın istemci kimliği belirtin.</span><span class="sxs-lookup"><span data-stu-id="93cdf-182">Specify hello application's client ID.</span></span> | <span data-ttu-id="93cdf-183">Evet</span><span class="sxs-lookup"><span data-stu-id="93cdf-183">Yes</span></span> |
| <span data-ttu-id="93cdf-184">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="93cdf-184">**servicePrincipalKey**</span></span> | <span data-ttu-id="93cdf-185">Merhaba uygulamanın anahtarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="93cdf-185">Specify hello application's key.</span></span> | <span data-ttu-id="93cdf-186">Evet</span><span class="sxs-lookup"><span data-stu-id="93cdf-186">Yes</span></span> |
| <span data-ttu-id="93cdf-187">**Kiracı**</span><span class="sxs-lookup"><span data-stu-id="93cdf-187">**tenant**</span></span> | <span data-ttu-id="93cdf-188">Uygulamanızın bulunduğu altında Hello Kiracı bilgileri (etki alanı adı veya Kiracı kimliği) belirtin.</span><span class="sxs-lookup"><span data-stu-id="93cdf-188">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="93cdf-189">Vurgulama hello fare hello sağ üst köşesindeki hello Azure portal tarafından alabilir.</span><span class="sxs-lookup"><span data-stu-id="93cdf-189">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="93cdf-190">Evet</span><span class="sxs-lookup"><span data-stu-id="93cdf-190">Yes</span></span> |

<span data-ttu-id="93cdf-191">**Örnek: Hizmet asıl kimlik doğrulaması**</span><span class="sxs-lookup"><span data-stu-id="93cdf-191">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="93cdf-192">Kullanıcı kimlik bilgileri doğrulaması</span><span class="sxs-lookup"><span data-stu-id="93cdf-192">User credential authentication</span></span>
<span data-ttu-id="93cdf-193">Alternatif olarak, aşağıdaki özelliklere hello belirterek kullanıcı kimlik bilgileri kimlik doğrulaması toocopy gelen veya tooData Lake Store kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="93cdf-193">Alternatively, you can use user credential authentication toocopy from or tooData Lake Store by specifying hello following properties:</span></span>

| <span data-ttu-id="93cdf-194">Özellik</span><span class="sxs-lookup"><span data-stu-id="93cdf-194">Property</span></span> | <span data-ttu-id="93cdf-195">Açıklama</span><span class="sxs-lookup"><span data-stu-id="93cdf-195">Description</span></span> | <span data-ttu-id="93cdf-196">Gerekli</span><span class="sxs-lookup"><span data-stu-id="93cdf-196">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="93cdf-197">**Yetkilendirme**</span><span class="sxs-lookup"><span data-stu-id="93cdf-197">**authorization**</span></span> | <span data-ttu-id="93cdf-198">Merhaba tıklatın **Authorize** hello Data Factory Düzenleyici'düğmesine tıklayın ve hello otomatik olarak oluşturulur yetkilendirme URL'si toothis özelliği atar kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="93cdf-198">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="93cdf-199">Evet</span><span class="sxs-lookup"><span data-stu-id="93cdf-199">Yes</span></span> |
| <span data-ttu-id="93cdf-200">**SessionID**</span><span class="sxs-lookup"><span data-stu-id="93cdf-200">**sessionId**</span></span> | <span data-ttu-id="93cdf-201">Merhaba OAuth yetkilendirme oturumundan OAuth oturum kimliği.</span><span class="sxs-lookup"><span data-stu-id="93cdf-201">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="93cdf-202">Her oturum kimliği benzersiz olup yalnızca bir kez kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="93cdf-202">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="93cdf-203">Merhaba Data Factory Düzenleyici kullandığınızda bu ayarı otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="93cdf-203">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="93cdf-204">Evet</span><span class="sxs-lookup"><span data-stu-id="93cdf-204">Yes</span></span> |

<span data-ttu-id="93cdf-205">**Örnek: Kullanıcı kimlik bilgileri doğrulaması**</span><span class="sxs-lookup"><span data-stu-id="93cdf-205">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="93cdf-206">Belirteç süre sonu</span><span class="sxs-lookup"><span data-stu-id="93cdf-206">Token expiration</span></span>
<span data-ttu-id="93cdf-207">Merhaba hello kullanarak oluşturmak yetkilendirme kodu **Authorize** düğmesi belirli bir miktar süre sonra süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="93cdf-207">hello authorization code that you generate by using hello **Authorize** button expires after a certain amount of time.</span></span> <span data-ttu-id="93cdf-208">iletiden hello hello kimlik doğrulama belirtecini süresi doldu anlamına gelir:</span><span class="sxs-lookup"><span data-stu-id="93cdf-208">hello following message means that hello authentication token has expired:</span></span>

<span data-ttu-id="93cdf-209">Kimlik bilgisi işlemi hatası: invalid_grant - AADSTS70002: Kimlik doğrulanırken hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="93cdf-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="93cdf-210">AADSTS70008: hello erişim izninin süresi doldu veya iptal sağlanan.</span><span class="sxs-lookup"><span data-stu-id="93cdf-210">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="93cdf-211">İzleme kimliği: d18629e8-af88-43c5-88e3-d8419eb1fca1 bağıntı kimliği: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 zaman damgası: 2015-12-15 21 09 31Z.</span><span class="sxs-lookup"><span data-stu-id="93cdf-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span></span>

<span data-ttu-id="93cdf-212">Merhaba aşağıdaki tabloda farklı türlerdeki kullanıcı hesapları hello sona erme sürelerini gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="93cdf-212">hello following table shows hello expiration times of different types of user accounts:</span></span>


| <span data-ttu-id="93cdf-213">Kullanıcı türü</span><span class="sxs-lookup"><span data-stu-id="93cdf-213">User type</span></span> | <span data-ttu-id="93cdf-214">Kullanım süresi sonu</span><span class="sxs-lookup"><span data-stu-id="93cdf-214">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="93cdf-215">Kullanıcı hesaplarını *değil* Azure Active Directory tarafından yönetilen (örneğin, @hotmail.com veya @live.com)</span><span class="sxs-lookup"><span data-stu-id="93cdf-215">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span></span> |<span data-ttu-id="93cdf-216">12 saat</span><span class="sxs-lookup"><span data-stu-id="93cdf-216">12 hours</span></span> |
| <span data-ttu-id="93cdf-217">Azure Active Directory tarafından yönetilen kullanıcılar hesapları</span><span class="sxs-lookup"><span data-stu-id="93cdf-217">Users accounts managed by Azure Active Directory</span></span> |<span data-ttu-id="93cdf-218">14 gün sonra hello son dilim çalıştırın</span><span class="sxs-lookup"><span data-stu-id="93cdf-218">14 days after hello last slice run</span></span> <br/><br/><span data-ttu-id="93cdf-219">90 OAuth tabanlı bir bağlantılı hizmette dayanan bir dilim 14 günde bir en az bir kez çalıştırıyorsa gün</span><span class="sxs-lookup"><span data-stu-id="93cdf-219">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span></span> |

<span data-ttu-id="93cdf-220">Merhaba belirteci süre sonu önce parolanızı değiştirirseniz, hello belirteci hemen süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="93cdf-220">If you change your password before hello token expiration time, hello token expires immediately.</span></span> <span data-ttu-id="93cdf-221">Bu bölümde daha önce bahsedilen hello iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="93cdf-221">You will see hello message mentioned earlier in this section.</span></span>

<span data-ttu-id="93cdf-222">Hello kullanarak hello hesabı yeniden yetkilendirmek **Authorize** tooredeploy hello hello belirtecinin süresi dolduğunda düğmesi bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="93cdf-222">You can reauthorize hello account by using hello **Authorize** button when hello token expires tooredeploy hello linked service.</span></span> <span data-ttu-id="93cdf-223">Merhaba değerlerini de oluşturabilirsiniz **SessionID** ve **yetkilendirme** kullanarak program aracılığıyla özellikleri hello kodu:</span><span class="sxs-lookup"><span data-stu-id="93cdf-223">You can also generate values for hello **sessionId** and **authorization** properties programmatically by using hello following code:</span></span>


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
<span data-ttu-id="93cdf-224">Merhaba hello kod içinde kullanılan hello Data Factory sınıfları hakkında daha fazla bilgi için bkz [AzureDataLakeStoreLinkedService sınıfı](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService sınıfı](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), ve [ AuthorizationSessionGetResponse sınıfı](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) Konular.</span><span class="sxs-lookup"><span data-stu-id="93cdf-224">For details about hello Data Factory classes used in hello code, see hello [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span></span> <span data-ttu-id="93cdf-225">Bir başvuru tooversion ekleme `2.9.10826.1824` , `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` hello için `WindowsFormsWebAuthenticationDialog` hello kod içinde kullanılan bir sınıftır.</span><span class="sxs-lookup"><span data-stu-id="93cdf-225">Add a reference tooversion `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for hello `WindowsFormsWebAuthenticationDialog` class used in hello code.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="93cdf-226">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="93cdf-226">Dataset properties</span></span>
<span data-ttu-id="93cdf-227">toospecify bir veri kümesi toorepresent girdi verileri Data Lake Store, ayarladığınız hello **türü** hello dataset özelliğinin çok**AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="93cdf-227">toospecify a dataset toorepresent input data in a Data Lake Store, you set hello **type** property of hello dataset too**AzureDataLakeStore**.</span></span> <span data-ttu-id="93cdf-228">Set hello **linkedServiceName** hello dataset toohello hello Data Lake Store adını özelliğinin bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="93cdf-228">Set hello **linkedServiceName** property of hello dataset toohello name of hello Data Lake Store linked service.</span></span> <span data-ttu-id="93cdf-229">Merhaba JSON bölümler ve veri kümelerini tanımlamak için kullanılabilen özellikler tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="93cdf-229">For a full list of JSON sections and properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="93cdf-230">JSON, bir veri kümesini bölümlerini gibi **yapısı**, **kullanılabilirlik**, ve **İlkesi**, tüm veri kümesi türleri için benzerdir (Azure SQL database, Azure blob ve Azure tablo için Örnek).</span><span class="sxs-lookup"><span data-stu-id="93cdf-230">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span></span> <span data-ttu-id="93cdf-231">Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve konum ve hello veri deposundaki hello veri biçimi gibi bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="93cdf-231">hello **typeProperties** section is different for each type of dataset and provides information such as location and format of hello data in hello data store.</span></span> 

<span data-ttu-id="93cdf-232">Merhaba **typeProperties** bir veri kümesi için bir bölüm türü **AzureDataLakeStore** aşağıdaki özelliklere hello içerir:</span><span class="sxs-lookup"><span data-stu-id="93cdf-232">hello **typeProperties** section for a dataset of type **AzureDataLakeStore** contains hello following properties:</span></span>

| <span data-ttu-id="93cdf-233">Özellik</span><span class="sxs-lookup"><span data-stu-id="93cdf-233">Property</span></span> | <span data-ttu-id="93cdf-234">Açıklama</span><span class="sxs-lookup"><span data-stu-id="93cdf-234">Description</span></span> | <span data-ttu-id="93cdf-235">Gerekli</span><span class="sxs-lookup"><span data-stu-id="93cdf-235">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="93cdf-236">**folderPath**</span><span class="sxs-lookup"><span data-stu-id="93cdf-236">**folderPath**</span></span> |<span data-ttu-id="93cdf-237">Yol toohello kapsayıcı ve Data Lake Store klasörü.</span><span class="sxs-lookup"><span data-stu-id="93cdf-237">Path toohello container and folder in Data Lake Store.</span></span> |<span data-ttu-id="93cdf-238">Evet</span><span class="sxs-lookup"><span data-stu-id="93cdf-238">Yes</span></span> |
| <span data-ttu-id="93cdf-239">**Dosya adı**</span><span class="sxs-lookup"><span data-stu-id="93cdf-239">**fileName**</span></span> |<span data-ttu-id="93cdf-240">Azure Data Lake Store'da hello dosyasının adı.</span><span class="sxs-lookup"><span data-stu-id="93cdf-240">Name of hello file in Azure Data Lake Store.</span></span> <span data-ttu-id="93cdf-241">Merhaba **fileName** özelliği isteğe bağlıdır ve büyük küçük harfe duyarlı.</span><span class="sxs-lookup"><span data-stu-id="93cdf-241">hello **fileName** property is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="93cdf-242">Belirtirseniz **fileName**, (kopyalama dahil) hello etkinlik hello belirli dosya üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="93cdf-242">If you specify **fileName**, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="93cdf-243">Zaman **fileName** belirtilmezse, kopyalama içeren tüm dosyaları **folderPath** hello girdi veri kümesi içinde.</span><span class="sxs-lookup"><span data-stu-id="93cdf-243">When **fileName** is not specified, Copy includes all files in **folderPath** in hello input dataset.</span></span><br/><br/><span data-ttu-id="93cdf-244">Zaman **fileName** bir çıkış veri kümesi için belirtilmemiş ve **preserveHierarchy** belirtilmedi etkinlik havuzunda hello oluşturulan hello dosyasının adıdır veri hello biçiminde. _GUID_.txt'.</span><span class="sxs-lookup"><span data-stu-id="93cdf-244">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello format Data._Guid_.txt\`.</span></span> <span data-ttu-id="93cdf-245">Örnek: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span><span class="sxs-lookup"><span data-stu-id="93cdf-245">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span></span> |<span data-ttu-id="93cdf-246">Hayır</span><span class="sxs-lookup"><span data-stu-id="93cdf-246">No</span></span> |
| <span data-ttu-id="93cdf-247">**partitionedBy**</span><span class="sxs-lookup"><span data-stu-id="93cdf-247">**partitionedBy**</span></span> |<span data-ttu-id="93cdf-248">Merhaba **partitionedBy** özelliği isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="93cdf-248">hello **partitionedBy** property is optional.</span></span> <span data-ttu-id="93cdf-249">Toospecify dinamik bir yol ve dosya adını time series verilerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93cdf-249">You can use it toospecify a dynamic path and file name for time-series data.</span></span> <span data-ttu-id="93cdf-250">Örneğin, **folderPath** için verileri saatte parametreli olabilir.</span><span class="sxs-lookup"><span data-stu-id="93cdf-250">For example, **folderPath** can be parameterized for every hour of data.</span></span> <span data-ttu-id="93cdf-251">Ayrıntılı bilgi ve örnekler için bkz: [hello partitionedBy özelliği](#using-partitionedby-property).</span><span class="sxs-lookup"><span data-stu-id="93cdf-251">For details and examples, see [hello partitionedBy property](#using-partitionedby-property).</span></span> |<span data-ttu-id="93cdf-252">Hayır</span><span class="sxs-lookup"><span data-stu-id="93cdf-252">No</span></span> |
| <span data-ttu-id="93cdf-253">**biçimi**</span><span class="sxs-lookup"><span data-stu-id="93cdf-253">**format**</span></span> | <span data-ttu-id="93cdf-254">şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, ve  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="93cdf-254">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="93cdf-255">Set hello **türü** altında özellik **biçimi** tooone bu değerleri.</span><span class="sxs-lookup"><span data-stu-id="93cdf-255">Set hello **type** property under **format** tooone of these values.</span></span> <span data-ttu-id="93cdf-256">Merhaba daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [JSON biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi ](data-factory-supported-file-and-compression-formats.md#parquet-format) hello bölümlerde [Azure Data Factory tarafından desteklenen dosya ve sıkıştırma biçimleri](data-factory-supported-file-and-compression-formats.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="93cdf-256">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in hello [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span> <br><br> <span data-ttu-id="93cdf-257">Toocopy dosyaları isterseniz "olarak-olan" Merhaba dosya tabanlı depoları arasında (ikili kopya), atla `format` iki girdi ve çıktı veri kümesi tanımları bölümünde.</span><span class="sxs-lookup"><span data-stu-id="93cdf-257">If you want toocopy files "as-is" between file-based stores (binary copy), skip hello `format` section in both input and output dataset definitions.</span></span> |<span data-ttu-id="93cdf-258">Hayır</span><span class="sxs-lookup"><span data-stu-id="93cdf-258">No</span></span> |
| <span data-ttu-id="93cdf-259">**sıkıştırma**</span><span class="sxs-lookup"><span data-stu-id="93cdf-259">**compression**</span></span> | <span data-ttu-id="93cdf-260">Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin.</span><span class="sxs-lookup"><span data-stu-id="93cdf-260">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="93cdf-261">Desteklenen türler **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="93cdf-261">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="93cdf-262">Desteklenen düzeyler **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="93cdf-262">Supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="93cdf-263">Daha fazla bilgi için bkz: [Azure Data Factory tarafından desteklenen dosya ve sıkıştırma biçimleri](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="93cdf-263">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="93cdf-264">Hayır</span><span class="sxs-lookup"><span data-stu-id="93cdf-264">No</span></span> |

### <a name="hello-partitionedby-property"></a><span data-ttu-id="93cdf-265">Merhaba partitionedBy özelliği</span><span class="sxs-lookup"><span data-stu-id="93cdf-265">hello partitionedBy property</span></span>
<span data-ttu-id="93cdf-266">Dinamik belirtebilirsiniz **folderPath** ve **fileName** hello zaman serisi verilerle özelliklerini **partitionedBy** özelliği, veri fabrikası işlevleri ve sistem değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="93cdf-266">You can specify dynamic **folderPath** and **fileName** properties for time-series data with hello **partitionedBy** property, Data Factory functions, and system variables.</span></span> <span data-ttu-id="93cdf-267">Merhaba Ayrıntılar için bkz [Azure Data Factory - işlevler ve sistem değişkenleri](data-factory-functions-variables.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="93cdf-267">For details, see hello [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span></span>


<span data-ttu-id="93cdf-268">Örneğin, aşağıdaki hello içinde `{Slice}` hello hello Data Factory sistem değişkeninin değeriyle değiştirilir `SliceStart` belirtilen hello biçiminde (`yyyyMMddHH`).</span><span class="sxs-lookup"><span data-stu-id="93cdf-268">In hello following example, `{Slice}` is replaced with hello value of hello Data Factory system variable `SliceStart` in hello format specified (`yyyyMMddHH`).</span></span> <span data-ttu-id="93cdf-269">Merhaba adı `SliceStart` toohello hello dilimin başlangıç zamanı gösterir.</span><span class="sxs-lookup"><span data-stu-id="93cdf-269">hello name `SliceStart` refers toohello start time of hello slice.</span></span> <span data-ttu-id="93cdf-270">Merhaba `folderPath` özelliktir giriş olarak her dilim için farklı `wikidatagateway/wikisampledataout/2014100103` veya `wikidatagateway/wikisampledataout/2014100104`.</span><span class="sxs-lookup"><span data-stu-id="93cdf-270">hello `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="93cdf-271">Aşağıdaki örnek, hello yıl, ay, gün ve saat hello içinde `SliceStart` hello tarafından kullanılan ayrı değişkenleri içine ayıklanan `folderPath` ve `fileName` özellikleri:</span><span class="sxs-lookup"><span data-stu-id="93cdf-271">In hello following example, hello year, month, day, and time of `SliceStart` are extracted into separate variables that are used by hello `folderPath` and `fileName` properties:</span></span>
```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="93cdf-272">Zaman serisi veri kümeleri hakkında daha fazla ayrıntı için zamanlama ve dilim hello bkz [Azure Data Factory'deki veri kümelerini](data-factory-create-datasets.md) ve [Data Factory zamanlama ve yürütme](data-factory-scheduling-and-execution.md) makaleleri.</span><span class="sxs-lookup"><span data-stu-id="93cdf-272">For more details on time-series datasets, scheduling, and slices, see hello [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="93cdf-273">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="93cdf-273">Copy activity properties</span></span>
<span data-ttu-id="93cdf-274">Merhaba bölümler ve etkinlikleri tanımlamak için kullanılabilen özellikler tam listesi için bkz [ardışık düzen oluşturma](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="93cdf-274">For a full list of sections and properties available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="93cdf-275">Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="93cdf-275">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="93cdf-276">Merhaba hello kullanılabilen özellikleri **typeProperties** bölüm etkinliğin her etkinlik türü ile değişir.</span><span class="sxs-lookup"><span data-stu-id="93cdf-276">hello properties available in hello **typeProperties** section of an activity vary with each activity type.</span></span> <span data-ttu-id="93cdf-277">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="93cdf-277">For a copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="93cdf-278">**AzureDataLakeStoreSource** hello özelliğinde aşağıdaki hello destekleyen **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="93cdf-278">**AzureDataLakeStoreSource** supports hello following property in hello **typeProperties** section:</span></span>

| <span data-ttu-id="93cdf-279">Özellik</span><span class="sxs-lookup"><span data-stu-id="93cdf-279">Property</span></span> | <span data-ttu-id="93cdf-280">Açıklama</span><span class="sxs-lookup"><span data-stu-id="93cdf-280">Description</span></span> | <span data-ttu-id="93cdf-281">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="93cdf-281">Allowed values</span></span> | <span data-ttu-id="93cdf-282">Gerekli</span><span class="sxs-lookup"><span data-stu-id="93cdf-282">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="93cdf-283">**özyinelemeli**</span><span class="sxs-lookup"><span data-stu-id="93cdf-283">**recursive**</span></span> |<span data-ttu-id="93cdf-284">Merhaba klasörlerdeki veya yalnızca klasörden hello belirtilen Hello veri yinelemeli olarak okunur olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="93cdf-284">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="93cdf-285">(Varsayılan değer) false değerini true</span><span class="sxs-lookup"><span data-stu-id="93cdf-285">True (default value), False</span></span> |<span data-ttu-id="93cdf-286">Hayır</span><span class="sxs-lookup"><span data-stu-id="93cdf-286">No</span></span> |


<span data-ttu-id="93cdf-287">**AzureDataLakeStoreSink** hello özelliklerinde aşağıdaki hello destekleyen **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="93cdf-287">**AzureDataLakeStoreSink** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="93cdf-288">Özellik</span><span class="sxs-lookup"><span data-stu-id="93cdf-288">Property</span></span> | <span data-ttu-id="93cdf-289">Açıklama</span><span class="sxs-lookup"><span data-stu-id="93cdf-289">Description</span></span> | <span data-ttu-id="93cdf-290">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="93cdf-290">Allowed values</span></span> | <span data-ttu-id="93cdf-291">Gerekli</span><span class="sxs-lookup"><span data-stu-id="93cdf-291">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="93cdf-292">**copyBehavior**</span><span class="sxs-lookup"><span data-stu-id="93cdf-292">**copyBehavior**</span></span> |<span data-ttu-id="93cdf-293">Merhaba kopyalama davranışını belirtir.</span><span class="sxs-lookup"><span data-stu-id="93cdf-293">Specifies hello copy behavior.</span></span> |<span data-ttu-id="93cdf-294"><b>PreserveHierarchy</b>: hello dosya hiyerarşisi hello hedef klasörde korur.</span><span class="sxs-lookup"><span data-stu-id="93cdf-294"><b>PreserveHierarchy</b>: Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="93cdf-295">Kaynak dosya toosource klasörünün göreli yolu Hello aynı toohello göreli hedef dosya tootarget klasör yoludur.</span><span class="sxs-lookup"><span data-stu-id="93cdf-295">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="93cdf-296"><b>FlattenHierarchy</b>: hello kaynak klasördeki tüm dosyaları hello ilk düzeyi hello hedef klasörü içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="93cdf-296"><b>FlattenHierarchy</b>: All files from hello source folder are created in hello first level of hello target folder.</span></span> <span data-ttu-id="93cdf-297">Merhaba hedef dosyaları otomatik olarak oluşturulur adlarıyla oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="93cdf-297">hello target files are created with autogenerated names.</span></span><br/><br/><span data-ttu-id="93cdf-298"><b>MergeFiles</b>: hello kaynak klasör tooone dosyasından tüm dosyaları birleştirir.</span><span class="sxs-lookup"><span data-stu-id="93cdf-298"><b>MergeFiles</b>: Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="93cdf-299">Merhaba dosya veya blob adı belirtilirse, hello belirtilen ad hello birleştirilmiş dosya adı değil.</span><span class="sxs-lookup"><span data-stu-id="93cdf-299">If hello file or blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="93cdf-300">Aksi takdirde hello dosya adı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="93cdf-300">Otherwise, hello file name is autogenerated.</span></span> |<span data-ttu-id="93cdf-301">Hayır</span><span class="sxs-lookup"><span data-stu-id="93cdf-301">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="93cdf-302">özyinelemeli ve copyBehavior örnekleri</span><span class="sxs-lookup"><span data-stu-id="93cdf-302">recursive and copyBehavior examples</span></span>
<span data-ttu-id="93cdf-303">Bu bölümde hello kopyalama işlemi farklı bir özyinelemeli ve copyBehavior değerleri kombinasyonu için sonuçta elde edilen davranışını hello açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="93cdf-303">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="93cdf-304">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="93cdf-304">recursive</span></span> | <span data-ttu-id="93cdf-305">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="93cdf-305">copyBehavior</span></span> | <span data-ttu-id="93cdf-306">Bunun sonucunda oluşan davranışı</span><span class="sxs-lookup"><span data-stu-id="93cdf-306">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="93cdf-307">TRUE</span><span class="sxs-lookup"><span data-stu-id="93cdf-307">true</span></span> |<span data-ttu-id="93cdf-308">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="93cdf-308">preserveHierarchy</span></span> |<span data-ttu-id="93cdf-309">Bir kaynak klasörü için Klasör1 yapı izlenerek hello ile:</span><span class="sxs-lookup"><span data-stu-id="93cdf-309">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="93cdf-310">Klasör1</span><span class="sxs-lookup"><span data-stu-id="93cdf-310">Folder1</span></span><br/><span data-ttu-id="93cdf-311">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="93cdf-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="93cdf-312">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="93cdf-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="93cdf-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="93cdf-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="93cdf-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="93cdf-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="93cdf-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="93cdf-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="93cdf-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="93cdf-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="93cdf-317">Merhaba hedef klasör Klasör1 aynı hello kaynağı olarak yapısı hello oluşturulur</span><span class="sxs-lookup"><span data-stu-id="93cdf-317">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="93cdf-318">Klasör1</span><span class="sxs-lookup"><span data-stu-id="93cdf-318">Folder1</span></span><br/><span data-ttu-id="93cdf-319">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="93cdf-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="93cdf-320">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="93cdf-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="93cdf-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="93cdf-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="93cdf-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="93cdf-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="93cdf-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="93cdf-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="93cdf-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="93cdf-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="93cdf-325">TRUE</span><span class="sxs-lookup"><span data-stu-id="93cdf-325">true</span></span> |<span data-ttu-id="93cdf-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="93cdf-326">flattenHierarchy</span></span> |<span data-ttu-id="93cdf-327">Bir kaynak klasörü için Klasör1 yapı izlenerek hello ile:</span><span class="sxs-lookup"><span data-stu-id="93cdf-327">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="93cdf-328">Klasör1</span><span class="sxs-lookup"><span data-stu-id="93cdf-328">Folder1</span></span><br/><span data-ttu-id="93cdf-329">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="93cdf-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="93cdf-330">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="93cdf-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="93cdf-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="93cdf-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="93cdf-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="93cdf-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="93cdf-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="93cdf-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="93cdf-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="93cdf-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="93cdf-335">Merhaba hedef Klasör1 yapı izlenerek hello ile oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="93cdf-335">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="93cdf-336">Klasör1</span><span class="sxs-lookup"><span data-stu-id="93cdf-336">Folder1</span></span><br/><span data-ttu-id="93cdf-337">&nbsp;&nbsp;&nbsp;&nbsp;dosya1 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="93cdf-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="93cdf-338">&nbsp;&nbsp;&nbsp;&nbsp;dosya2 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="93cdf-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="93cdf-339">&nbsp;&nbsp;&nbsp;&nbsp;dosya3 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="93cdf-339">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="93cdf-340">&nbsp;&nbsp;&nbsp;&nbsp;File4 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="93cdf-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="93cdf-341">&nbsp;&nbsp;&nbsp;&nbsp;File5 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="93cdf-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="93cdf-342">TRUE</span><span class="sxs-lookup"><span data-stu-id="93cdf-342">true</span></span> |<span data-ttu-id="93cdf-343">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="93cdf-343">mergeFiles</span></span> |<span data-ttu-id="93cdf-344">Bir kaynak klasörü için Klasör1 yapı izlenerek hello ile:</span><span class="sxs-lookup"><span data-stu-id="93cdf-344">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="93cdf-345">Klasör1</span><span class="sxs-lookup"><span data-stu-id="93cdf-345">Folder1</span></span><br/><span data-ttu-id="93cdf-346">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="93cdf-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="93cdf-347">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="93cdf-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="93cdf-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="93cdf-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="93cdf-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="93cdf-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="93cdf-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="93cdf-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="93cdf-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="93cdf-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="93cdf-352">Merhaba hedef Klasör1 yapı izlenerek hello ile oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="93cdf-352">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="93cdf-353">Klasör1</span><span class="sxs-lookup"><span data-stu-id="93cdf-353">Folder1</span></span><br/><span data-ttu-id="93cdf-354">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1 + dosya2 + dosya3 + File4 + 5 dosyası içeriği otomatik olarak oluşturulan dosya adında bir dosya halinde birleştirilir</span><span class="sxs-lookup"><span data-stu-id="93cdf-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="93cdf-355">False</span><span class="sxs-lookup"><span data-stu-id="93cdf-355">false</span></span> |<span data-ttu-id="93cdf-356">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="93cdf-356">preserveHierarchy</span></span> |<span data-ttu-id="93cdf-357">Bir kaynak klasörü için Klasör1 yapı izlenerek hello ile:</span><span class="sxs-lookup"><span data-stu-id="93cdf-357">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="93cdf-358">Klasör1</span><span class="sxs-lookup"><span data-stu-id="93cdf-358">Folder1</span></span><br/><span data-ttu-id="93cdf-359">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="93cdf-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="93cdf-360">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="93cdf-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="93cdf-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="93cdf-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="93cdf-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="93cdf-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="93cdf-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="93cdf-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="93cdf-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="93cdf-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="93cdf-365">Merhaba hedef klasör Klasör1 yapı izlenerek hello ile oluşturulur</span><span class="sxs-lookup"><span data-stu-id="93cdf-365">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="93cdf-366">Klasör1</span><span class="sxs-lookup"><span data-stu-id="93cdf-366">Folder1</span></span><br/><span data-ttu-id="93cdf-367">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="93cdf-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="93cdf-368">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="93cdf-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="93cdf-369">Dosya3, File4 ve File5 Subfolder1 değil toplanma.</span><span class="sxs-lookup"><span data-stu-id="93cdf-369">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="93cdf-370">False</span><span class="sxs-lookup"><span data-stu-id="93cdf-370">false</span></span> |<span data-ttu-id="93cdf-371">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="93cdf-371">flattenHierarchy</span></span> |<span data-ttu-id="93cdf-372">Bir kaynak klasörü için Klasör1 yapı izlenerek hello ile:</span><span class="sxs-lookup"><span data-stu-id="93cdf-372">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="93cdf-373">Klasör1</span><span class="sxs-lookup"><span data-stu-id="93cdf-373">Folder1</span></span><br/><span data-ttu-id="93cdf-374">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="93cdf-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="93cdf-375">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="93cdf-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="93cdf-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="93cdf-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="93cdf-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="93cdf-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="93cdf-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="93cdf-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="93cdf-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="93cdf-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="93cdf-380">Merhaba hedef klasör Klasör1 yapı izlenerek hello ile oluşturulur</span><span class="sxs-lookup"><span data-stu-id="93cdf-380">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="93cdf-381">Klasör1</span><span class="sxs-lookup"><span data-stu-id="93cdf-381">Folder1</span></span><br/><span data-ttu-id="93cdf-382">&nbsp;&nbsp;&nbsp;&nbsp;dosya1 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="93cdf-382">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="93cdf-383">&nbsp;&nbsp;&nbsp;&nbsp;dosya2 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="93cdf-383">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="93cdf-384">Dosya3, File4 ve File5 Subfolder1 değil toplanma.</span><span class="sxs-lookup"><span data-stu-id="93cdf-384">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="93cdf-385">False</span><span class="sxs-lookup"><span data-stu-id="93cdf-385">false</span></span> |<span data-ttu-id="93cdf-386">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="93cdf-386">mergeFiles</span></span> |<span data-ttu-id="93cdf-387">Bir kaynak klasörü için Klasör1 yapı izlenerek hello ile:</span><span class="sxs-lookup"><span data-stu-id="93cdf-387">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="93cdf-388">Klasör1</span><span class="sxs-lookup"><span data-stu-id="93cdf-388">Folder1</span></span><br/><span data-ttu-id="93cdf-389">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="93cdf-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="93cdf-390">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="93cdf-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="93cdf-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="93cdf-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="93cdf-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="93cdf-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="93cdf-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="93cdf-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="93cdf-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="93cdf-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="93cdf-395">Merhaba hedef klasör Klasör1 yapı izlenerek hello ile oluşturulur</span><span class="sxs-lookup"><span data-stu-id="93cdf-395">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="93cdf-396">Klasör1</span><span class="sxs-lookup"><span data-stu-id="93cdf-396">Folder1</span></span><br/><span data-ttu-id="93cdf-397">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1 + dosya2 içeriği otomatik olarak oluşturulan dosya adında bir dosya halinde birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="93cdf-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="93cdf-398">dosya1 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="93cdf-398">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="93cdf-399">Dosya3, File4 ve File5 Subfolder1 değil toplanma.</span><span class="sxs-lookup"><span data-stu-id="93cdf-399">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="93cdf-400">Desteklenen dosya ve sıkıştırma biçimleri</span><span class="sxs-lookup"><span data-stu-id="93cdf-400">Supported file and compression formats</span></span>
<span data-ttu-id="93cdf-401">Merhaba Ayrıntılar için bkz [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="93cdf-401">For details, see hello [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a><span data-ttu-id="93cdf-402">Veri tooand Data Lake Deposu'ndan veri kopyalamak için JSON örnekleri</span><span class="sxs-lookup"><span data-stu-id="93cdf-402">JSON examples for copying data tooand from Data Lake Store</span></span>
<span data-ttu-id="93cdf-403">Merhaba örnekleri aşağıdaki örnek JSON tanımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="93cdf-403">hello following examples provide sample JSON definitions.</span></span> <span data-ttu-id="93cdf-404">Bu örnek tanımları toocreate bir ardışık düzen hello kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="93cdf-404">You can use these sample definitions toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="93cdf-405">örneklerde nasıl hello toocopy veri tooand Data Lake Store ve Azure Blob depolama biriminden.</span><span class="sxs-lookup"><span data-stu-id="93cdf-405">hello examples show how toocopy data tooand from Data Lake Store and Azure Blob storage.</span></span> <span data-ttu-id="93cdf-406">Ancak, veriler kopyalanabilir _doğrudan_ herhangi birinden hello kaynakları tooany desteklenen hello havuzlarını biri.</span><span class="sxs-lookup"><span data-stu-id="93cdf-406">However, data can be copied _directly_ from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="93cdf-407">Daha fazla bilgi için "desteklenen veri depoları ve biçimleri" Merhaba bölümüne hello bkz [Kopyala etkinliğini kullanarak veri taşıma](data-factory-data-movement-activities.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="93cdf-407">For more information, see hello section "Supported data stores and formats" in hello [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span></span>  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a><span data-ttu-id="93cdf-408">Örnek: verileri Azure Blob Storage tooAzure Data Lake Store kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="93cdf-408">Example: Copy data from Azure Blob Storage tooAzure Data Lake Store</span></span>
<span data-ttu-id="93cdf-409">Bu bölümdeki kod Hello örneği gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="93cdf-409">hello example code in this section shows:</span></span>

* <span data-ttu-id="93cdf-410">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="93cdf-410">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="93cdf-411">Bağlı hizmet türü [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="93cdf-411">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="93cdf-412">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="93cdf-412">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="93cdf-413">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="93cdf-413">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="93cdf-414">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) ve [AzureDataLakeStoreSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="93cdf-414">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="93cdf-415">Merhaba örnekler ne zaman serisi verileri Azure Blob depolama biriminden göstermek tooData Lake Store saatte kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="93cdf-415">hello examples show how time-series data from Azure Blob Storage is copied tooData Lake Store every hour.</span></span> 

<span data-ttu-id="93cdf-416">**Azure Storage bağlı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="93cdf-416">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="93cdf-417">**Azure Data Lake Store hizmeti bağlı**</span><span class="sxs-lookup"><span data-stu-id="93cdf-417">**Azure Data Lake Store linked service**</span></span>

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="93cdf-418">Merhaba yapılandırma ayrıntıları için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="93cdf-418">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="93cdf-419">**Azure Blob girdi veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="93cdf-419">**Azure blob input dataset**</span></span>

<span data-ttu-id="93cdf-420">Aşağıdaki örneğine hello veri yeni blob üzerinden saatte kayıt (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="93cdf-420">In hello following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="93cdf-421">Merhaba klasör yolu ve dosya adını hello blob dinamik olarak değerlendirilir işleniyor hello dilimin hello başlangıç zamanı temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="93cdf-421">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="93cdf-422">Merhaba klasör yolu hello yıl, ay ve gün kısmı hello başlangıç saati kullanır.</span><span class="sxs-lookup"><span data-stu-id="93cdf-422">hello folder path uses hello year, month, and day portion of hello start time.</span></span> <span data-ttu-id="93cdf-423">Merhaba dosya adı hello saat hello kısmı başlangıç saati kullanır.</span><span class="sxs-lookup"><span data-stu-id="93cdf-423">hello file name uses hello hour portion of hello start time.</span></span> <span data-ttu-id="93cdf-424">Merhaba `"external": true` ayarı bildirir hello Data Factory hizmetinin bu hello tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="93cdf-424">hello `"external": true` setting informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

<span data-ttu-id="93cdf-425">**Azure Data Lake Store çıkış dataset**</span><span class="sxs-lookup"><span data-stu-id="93cdf-425">**Azure Data Lake Store output dataset**</span></span>

<span data-ttu-id="93cdf-426">Aşağıdaki örnek kopya veri tooData Lake deposu hello.</span><span class="sxs-lookup"><span data-stu-id="93cdf-426">hello following example copies data tooData Lake Store.</span></span> <span data-ttu-id="93cdf-427">Yeni veri kopyalanır tooData Lake Store her saat.</span><span class="sxs-lookup"><span data-stu-id="93cdf-427">New data is copied tooData Lake Store every hour.</span></span>

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


<span data-ttu-id="93cdf-428">**Bir blob kaynağı ve Data Lake Store havuz sahip işlem hattı kopyalama etkinliği**</span><span class="sxs-lookup"><span data-stu-id="93cdf-428">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span></span>

<span data-ttu-id="93cdf-429">Aşağıdaki örneğine hello hello ardışık düzen yapılandırılmış bir kopyalama etkinliği içeren toouse hello girdi ve çıktı veri kümeleri.</span><span class="sxs-lookup"><span data-stu-id="93cdf-429">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="93cdf-430">Merhaba kopyalama etkinliği zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="93cdf-430">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="93cdf-431">JSON tanımını Hello ardışık düzeninde, hello `source` türü olarak ayarlanmış çok`BlobSource`ve hello `sink` türü olarak ayarlanmış çok`AzureDataLakeStoreSink`.</span><span class="sxs-lookup"><span data-stu-id="93cdf-431">In hello pipeline JSON definition, hello `source` type is set too`BlobSource`, and hello `sink` type is set too`AzureDataLakeStoreSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
        ]
    }
}
```

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a><span data-ttu-id="93cdf-432">Örnek: Verilerini Azure Data Lake Store tooan Azure blob</span><span class="sxs-lookup"><span data-stu-id="93cdf-432">Example: Copy data from Azure Data Lake Store tooan Azure blob</span></span>
<span data-ttu-id="93cdf-433">Bu bölümdeki kod Hello örneği gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="93cdf-433">hello example code in this section shows:</span></span>

* <span data-ttu-id="93cdf-434">Bağlı hizmet türü [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="93cdf-434">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="93cdf-435">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="93cdf-435">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="93cdf-436">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="93cdf-436">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="93cdf-437">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="93cdf-437">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="93cdf-438">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [AzureDataLakeStoreSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="93cdf-438">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="93cdf-439">Merhaba kodu time series verilerini her saat Data Lake Store tooan Azure blob ' kopyalar.</span><span class="sxs-lookup"><span data-stu-id="93cdf-439">hello code copies time-series data from Data Lake Store tooan Azure blob every hour.</span></span> 

<span data-ttu-id="93cdf-440">**Azure Data Lake Store hizmeti bağlı**</span><span class="sxs-lookup"><span data-stu-id="93cdf-440">**Azure Data Lake Store linked service**</span></span>

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="93cdf-441">Merhaba yapılandırma ayrıntıları için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="93cdf-441">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="93cdf-442">**Azure Storage bağlı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="93cdf-442">**Azure Storage linked service**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="93cdf-443">**Azure Data Lake girdi veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="93cdf-443">**Azure Data Lake input dataset**</span></span>

<span data-ttu-id="93cdf-444">Bu örnekte, ayarı `"external"` çok`true` hello Data Factory hizmetinin bu hello tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil bildirir.</span><span class="sxs-lookup"><span data-stu-id="93cdf-444">In this example, setting `"external"` too`true` informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
              "interval": 1
        },
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
<span data-ttu-id="93cdf-445">**Azure Blob çıktı veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="93cdf-445">**Azure blob output dataset**</span></span>

<span data-ttu-id="93cdf-446">Aşağıdaki örneğine hello veriler her saat tooa yeni blob yazılır (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="93cdf-446">In hello following example, data is written tooa new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="93cdf-447">hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="93cdf-447">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="93cdf-448">Merhaba klasör yolu hello yıl, ay, gün ve saat bölümünü hello başlangıç saati kullanır.</span><span class="sxs-lookup"><span data-stu-id="93cdf-448">hello folder path uses hello year, month, day, and hours portion of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="93cdf-449">**Bir Azure Data Lake Store kaynak ve blob havuz sahip işlem hattı kopyalama etkinliği**</span><span class="sxs-lookup"><span data-stu-id="93cdf-449">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span></span>

<span data-ttu-id="93cdf-450">Aşağıdaki örneğine hello hello ardışık düzen yapılandırılmış bir kopyalama etkinliği içeren toouse hello girdi ve çıktı veri kümeleri.</span><span class="sxs-lookup"><span data-stu-id="93cdf-450">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="93cdf-451">Merhaba kopyalama etkinliği zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="93cdf-451">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="93cdf-452">JSON tanımını Hello ardışık düzeninde, hello `source` türü olarak ayarlanmış çok`AzureDataLakeStoreSource`ve hello `sink` türü olarak ayarlanmış çok`BlobSink`.</span><span class="sxs-lookup"><span data-stu-id="93cdf-452">In hello pipeline JSON definition, hello `source` type is set too`AzureDataLakeStoreSource`, and hello `sink` type is set too`BlobSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
         ]
    }
}
```

<span data-ttu-id="93cdf-453">Merhaba kopyalama etkinlik tanımında hello kaynak dataset toocolumns hello havuz kümesindeki sütunlarından eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93cdf-453">In hello copy activity definition, you can also map columns from hello source dataset toocolumns in hello sink dataset.</span></span> <span data-ttu-id="93cdf-454">Ayrıntılar için bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="93cdf-454">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="93cdf-455">Performans ve ayar</span><span class="sxs-lookup"><span data-stu-id="93cdf-455">Performance and tuning</span></span>
<span data-ttu-id="93cdf-456">Kopyalama etkinliği performansı etkileyen hello Etkenler hakkında toolearn ve nasıl toooptimize, hello bkz [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="93cdf-456">toolearn about hello factors that affect Copy Activity performance and how toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span></span>
