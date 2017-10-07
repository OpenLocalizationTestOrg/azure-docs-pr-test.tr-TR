---
title: Azure Data Factory kullanarak bir dosya sistemi/aaaCopy verileri | Microsoft Docs
description: "Bilgi nasıl toocopy veri tooand Azure Data Factory kullanarak bir şirket içi dosya sisteminden."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="c87a1-103">Azure Data Factory kullanarak veri tooand bir şirket içi dosya sisteminden kopyalama</span><span class="sxs-lookup"><span data-stu-id="c87a1-103">Copy data tooand from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="c87a1-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toocopy veri grafikten bir şirket içi dosya sistemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c87a1-104">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data to/from an on-premises file system.</span></span> <span data-ttu-id="c87a1-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="c87a1-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="c87a1-106">Desteklenen senaryolar</span><span class="sxs-lookup"><span data-stu-id="c87a1-106">Supported scenarios</span></span>
<span data-ttu-id="c87a1-107">Veri kopyalama **bir şirket içi dosya sisteminden** veri depolarına aşağıdaki toohello:</span><span class="sxs-lookup"><span data-stu-id="c87a1-107">You can copy data **from an on-premises file system** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="c87a1-108">Veri depoları aşağıdaki hello verileri kopyalayabilirsiniz **tooan şirket içi dosya sistemi**:</span><span class="sxs-lookup"><span data-stu-id="c87a1-108">You can copy data from hello following data stores **tooan on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="c87a1-109">Başarıyla kopyalanan toohello hedef tamamlandıktan sonra kopyalama etkinliği hello kaynak dosyayı silmez.</span><span class="sxs-lookup"><span data-stu-id="c87a1-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="c87a1-110">Sonra başarılı bir kopyasını toodelete hello kaynak dosyası gerekiyorsa, bir özel etkinlik toodelete hello dosyası oluşturun ve hello ardışık düzeninde hello etkinliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="c87a1-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="c87a1-111">Bağlantıyı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c87a1-111">Enabling connectivity</span></span>
<span data-ttu-id="c87a1-112">Veri Fabrikası destekleyen bir şirket içi dosya sisteminden bağlanan tooand **veri yönetimi ağ geçidi**.</span><span class="sxs-lookup"><span data-stu-id="c87a1-112">Data Factory supports connecting tooand from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="c87a1-113">Dosya sistemi dahil olmak üzere hello Data Factory hizmeti tooconnect tooany desteklenen şirket içi veri depolama için şirket içi ortamınızda hello veri yönetimi ağ geçidi yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-113">You must install hello Data Management Gateway in your on-premises environment for hello Data Factory service tooconnect tooany supported on-premises data store including file system.</span></span> <span data-ttu-id="c87a1-114">toolearn veri yönetimi ağ geçidi hakkında ve hello ağ geçidi, ayarlama hakkında adım adım yönergeler için bkz: [şirket içi kaynakları ve veri yönetimi ağ geçidi ile Merhaba bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="c87a1-114">toolearn about Data Management Gateway and for step-by-step instructions on setting up hello gateway, see [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="c87a1-115">Veri Yönetimi ağ geçidi dışında herhangi bir ikili dosyaları yüklü toobe toocommunicate tooand bir şirket içi dosya sisteminden gerekir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-115">Apart from Data Management Gateway, no other binary files need toobe installed toocommunicate tooand from an on-premises file system.</span></span> <span data-ttu-id="c87a1-116">Yüklemeniz ve Azure Iaas sanal hello dosya sistemi olsa bile, hello veri yönetimi ağ geçidi kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-116">You must install and use hello Data Management Gateway even if hello file system is in Azure IaaS VM.</span></span> <span data-ttu-id="c87a1-117">Merhaba ağ geçidi hakkında ayrıntılı bilgi için bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="c87a1-117">For detailed information about hello gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="c87a1-118">toouse Linux dosya paylaşımı yükleme [Samba](https://www.samba.org/) Linux sunucusu ve Windows Server yükleme veri yönetimi ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="c87a1-118">toouse a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="c87a1-119">Veri Yönetimi ağ geçidi Linux sunucusu üzerinde yüklenmesi desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="c87a1-119">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c87a1-120">Başlarken</span><span class="sxs-lookup"><span data-stu-id="c87a1-120">Getting started</span></span>
<span data-ttu-id="c87a1-121">Farklı araçlar/API'lerini kullanarak verileri öğesine/öğesinden bir dosya sistemi taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c87a1-121">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="c87a1-122">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="c87a1-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="c87a1-123">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="c87a1-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="c87a1-124">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="c87a1-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c87a1-125">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="c87a1-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="c87a1-126">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c87a1-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="c87a1-127">Oluşturma bir **veri fabrikası**.</span><span class="sxs-lookup"><span data-stu-id="c87a1-127">Create a **data factory**.</span></span> <span data-ttu-id="c87a1-128">Veri Fabrikası bir veya daha fazla ardışık düzen içerebilir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="c87a1-129">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="c87a1-129">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="c87a1-130">Bir Azure blob depolama tooan şirket içi dosya sisteminden veri kopyalama, örneğin, iki bağlı hizmet toolink şirket içi dosya sistemi ve Azure depolama hesabı tooyour veri fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c87a1-130">For example, if you are copying data from an Azure blob storage tooan on-premises file system, you create two linked services toolink your on-premises file system and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="c87a1-131">Belirli tooan şirket içi dosya sistemi bağlantılı hizmet özellikler için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="c87a1-131">For linked service properties that are specific tooan on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="c87a1-132">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="c87a1-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="c87a1-133">Merhaba son adımda bahsedilen hello örnekte, bir veri kümesi toospecify hello blob kapsayıcısı ve hello giriş verisi içeren klasörü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c87a1-133">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="c87a1-134">Ve başka bir veri kümesi toospecify hello klasör ve dosya adı (isteğe bağlı) dosya sisteminizi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c87a1-134">And, you create another dataset toospecify hello folder and file name (optional) in your file system.</span></span> <span data-ttu-id="c87a1-135">Belirli tooon içi veri kümesi özellikleri dosya sistemi için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="c87a1-135">For dataset properties that are specific tooon-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="c87a1-136">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="c87a1-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="c87a1-137">Daha önce bahsedilen hello örnekte BlobSource bir kaynak ve FileSystemSink havuzu olarak hello kopya etkinliği için kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="c87a1-137">In hello example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for hello copy activity.</span></span> <span data-ttu-id="c87a1-138">Şirket içi dosya sistemi tooAzure Blob Depolama kopyalıyorsanız benzer şekilde, FileSystemSource ve BlobSink hello kopyalama etkinliği kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="c87a1-138">Similarly, if you are copying from on-premises file system tooAzure Blob Storage, you use FileSystemSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="c87a1-139">Belirli tooon içi kopyalama etkinliği özellikleri dosya sistemi için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="c87a1-139">For copy activity properties that are specific tooon-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="c87a1-140">Nasıl toouse bir veri deposu bir kaynak veya bir havuz olarak hakkında daha fazla bilgi için veri deposu hello önceki bölümdeki hello bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c87a1-140">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="c87a1-141">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c87a1-141">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="c87a1-142">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="c87a1-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="c87a1-143">Bir dosya sistemi/kullanılan toocopy verileri olan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples-for-copying-data-to-and-from-file-system) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="c87a1-143">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="c87a1-144">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli toofile sistem JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="c87a1-144">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific toofile system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c87a1-145">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="c87a1-145">Linked service properties</span></span>
<span data-ttu-id="c87a1-146">Bir şirket içi dosya sistemi tooan Azure data factory hello ile bağlayabilirsiniz **şirket içi dosya sunucusu** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="c87a1-146">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="c87a1-147">Aşağıdaki tablonun hello belirli toohello şirket içi dosya sunucusuna bağlı hizmeti olan JSON öğeleri için açıklamalar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c87a1-147">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="c87a1-148">Özellik</span><span class="sxs-lookup"><span data-stu-id="c87a1-148">Property</span></span> | <span data-ttu-id="c87a1-149">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c87a1-149">Description</span></span> | <span data-ttu-id="c87a1-150">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c87a1-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c87a1-151">type</span><span class="sxs-lookup"><span data-stu-id="c87a1-151">type</span></span> |<span data-ttu-id="c87a1-152">Merhaba type özelliği çok ayarlandığından emin olun**OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="c87a1-152">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="c87a1-153">Evet</span><span class="sxs-lookup"><span data-stu-id="c87a1-153">Yes</span></span> |
| <span data-ttu-id="c87a1-154">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="c87a1-154">host</span></span> |<span data-ttu-id="c87a1-155">Toocopy istediğiniz hello klasörü Hello kök yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-155">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="c87a1-156">Merhaba kaçış karakteri kullanmak ' \ ' hello dize özel karakter.</span><span class="sxs-lookup"><span data-stu-id="c87a1-156">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="c87a1-157">Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="c87a1-157">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="c87a1-158">Evet</span><span class="sxs-lookup"><span data-stu-id="c87a1-158">Yes</span></span> |
| <span data-ttu-id="c87a1-159">Kullanıcı Kimliği</span><span class="sxs-lookup"><span data-stu-id="c87a1-159">userid</span></span> |<span data-ttu-id="c87a1-160">Merhaba erişim toohello sunucusuna sahip hello kullanıcı Kimliğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="c87a1-160">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="c87a1-161">Hayır (encryptedCredential seçerseniz)</span><span class="sxs-lookup"><span data-stu-id="c87a1-161">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="c87a1-162">password</span><span class="sxs-lookup"><span data-stu-id="c87a1-162">password</span></span> |<span data-ttu-id="c87a1-163">Merhaba kullanıcı (UserID) Hello parolasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="c87a1-163">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="c87a1-164">Hayır (encryptedCredential seçerseniz</span><span class="sxs-lookup"><span data-stu-id="c87a1-164">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="c87a1-165">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="c87a1-165">encryptedCredential</span></span> |<span data-ttu-id="c87a1-166">Merhaba yeni AzureRmDataFactoryEncryptValue cmdlet'ini çalıştırarak alabilirsiniz hello şifreli kimlik bilgilerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="c87a1-166">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="c87a1-167">Hayır (toospecify kullanıcı kimliği ve parola düz metin olarak seçerseniz)</span><span class="sxs-lookup"><span data-stu-id="c87a1-167">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="c87a1-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="c87a1-168">gatewayName</span></span> |<span data-ttu-id="c87a1-169">Veri Fabrikası tooconnect toohello şirket içi dosya sunucusu kullanmalısınız hello ağ geçidi Hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-169">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="c87a1-170">Evet</span><span class="sxs-lookup"><span data-stu-id="c87a1-170">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="c87a1-171">Örnek bağlantılı hizmet ve veri kümesi tanımları</span><span class="sxs-lookup"><span data-stu-id="c87a1-171">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="c87a1-172">Senaryo</span><span class="sxs-lookup"><span data-stu-id="c87a1-172">Scenario</span></span> | <span data-ttu-id="c87a1-173">Bağlantılı hizmet tanımında ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="c87a1-173">Host in linked service definition</span></span> | <span data-ttu-id="c87a1-174">veri kümesi tanımında folderPath</span><span class="sxs-lookup"><span data-stu-id="c87a1-174">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c87a1-175">Veri Yönetimi ağ geçidi makine üzerinde yerel klasör:</span><span class="sxs-lookup"><span data-stu-id="c87a1-175">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="c87a1-176">Örnekler: D:\\ \* veya D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="c87a1-176">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="c87a1-177">D:\\ \\ (için veri yönetimi ağ geçidi 2.0 ve sonraki sürümler)</span><span class="sxs-lookup"><span data-stu-id="c87a1-177">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="c87a1-178">localhost (daha önceki sürümler için veri yönetimi ağ geçidi 2. 0)</span><span class="sxs-lookup"><span data-stu-id="c87a1-178">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="c87a1-179">. \\ \\ veya klasör\\\\alt klasör (için veri yönetimi ağ geçidi 2.0 ve sonraki sürümler)</span><span class="sxs-lookup"><span data-stu-id="c87a1-179">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="c87a1-180">D:\\ \\ veya D:\\\\klasörü\\\\alt klasör (için ağ geçidi sürüm 2.0 altında)</span><span class="sxs-lookup"><span data-stu-id="c87a1-180">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="c87a1-181">Uzak paylaşılan klasör:</span><span class="sxs-lookup"><span data-stu-id="c87a1-181">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="c87a1-182">Örnekler: \\ \\myserver\\paylaşmak\\ \* veya \\ \\myserver\\paylaşmak\\klasörü\\alt klasör\\*</span><span class="sxs-lookup"><span data-stu-id="c87a1-182">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="c87a1-183">\\\\\\\\myserver\\\\paylaşma</span><span class="sxs-lookup"><span data-stu-id="c87a1-183">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="c87a1-184">. \\ \\ veya klasör\\\\alt klasör</span><span class="sxs-lookup"><span data-stu-id="c87a1-184">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="c87a1-185">Örnek: kullanıcı adı ve parola düz metin olarak kullanma</span><span class="sxs-lookup"><span data-stu-id="c87a1-185">Example: Using username and password in plain text</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="c87a1-186">Örnek: encryptedcredential kullanma</span><span class="sxs-lookup"><span data-stu-id="c87a1-186">Example: Using encryptedcredential</span></span>

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="c87a1-187">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="c87a1-187">Dataset properties</span></span>
<span data-ttu-id="c87a1-188">Bölümleri ve veri kümelerini tanımlamak için kullanılabilir olan özellikleri tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="c87a1-188">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="c87a1-189">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri kümesi türleri için benzerdir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="c87a1-190">Merhaba typeProperties bölüm veri kümesi her tür için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="c87a1-190">hello typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="c87a1-191">Başlangıç konumu ve hello veri deposundaki hello veri biçimi gibi bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="c87a1-191">It provides information such as hello location and format of hello data in hello data store.</span></span> <span data-ttu-id="c87a1-192">Merhaba typeProperties bölüm türü hello veri kümesi için **FileShare** hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="c87a1-192">hello typeProperties section for hello dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="c87a1-193">Özellik</span><span class="sxs-lookup"><span data-stu-id="c87a1-193">Property</span></span> | <span data-ttu-id="c87a1-194">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c87a1-194">Description</span></span> | <span data-ttu-id="c87a1-195">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c87a1-195">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c87a1-196">folderPath</span><span class="sxs-lookup"><span data-stu-id="c87a1-196">folderPath</span></span> |<span data-ttu-id="c87a1-197">Merhaba alt toohello klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-197">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="c87a1-198">Merhaba kaçış karakteri kullanmak ' \' hello dize özel karakter.</span><span class="sxs-lookup"><span data-stu-id="c87a1-198">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="c87a1-199">Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="c87a1-199">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="c87a1-200">Bu özellik ile birleştirebilirsiniz **partitionBy** toohave klasör yolları dilimine göre başlangıç/bitiş tarih saatleri.</span><span class="sxs-lookup"><span data-stu-id="c87a1-200">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="c87a1-201">Evet</span><span class="sxs-lookup"><span data-stu-id="c87a1-201">Yes</span></span> |
| <span data-ttu-id="c87a1-202">fileName</span><span class="sxs-lookup"><span data-stu-id="c87a1-202">fileName</span></span> |<span data-ttu-id="c87a1-203">Hello Hello hello dosyasının adını belirtin **folderPath** hello tablo toorefer tooa belirli dosya hello klasöründeki istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="c87a1-203">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="c87a1-204">Bu özellik için herhangi bir değer belirtmezseniz, hello tablo hello klasöründeki tooall dosyaları işaret eder.</span><span class="sxs-lookup"><span data-stu-id="c87a1-204">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="c87a1-205">Zaman **fileName** bir çıkış veri kümesi için belirtilmemiş ve **preserveHierarchy** belirtilmedi etkinlik havuzunda hello oluşturulan hello dosyasının adıdır biçimini izleyen hello:</span><span class="sxs-lookup"><span data-stu-id="c87a1-205">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="c87a1-206">`Data.<Guid>.txt`(Örnek: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="c87a1-206">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="c87a1-207">Hayır</span><span class="sxs-lookup"><span data-stu-id="c87a1-207">No</span></span> |
| <span data-ttu-id="c87a1-208">fileFilter</span><span class="sxs-lookup"><span data-stu-id="c87a1-208">fileFilter</span></span> |<span data-ttu-id="c87a1-209">Tüm dosyalar yerine hello folderPath dosyaları kümesini filtre toobe tooselect kullanılan belirtin.</span><span class="sxs-lookup"><span data-stu-id="c87a1-209">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="c87a1-210">İzin verilen değerler: `*` (birden çok karakter) ve `?` (tek bir karakter).</span><span class="sxs-lookup"><span data-stu-id="c87a1-210">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="c87a1-211">Örnek 1: "fileFilter": "* .log"</span><span class="sxs-lookup"><span data-stu-id="c87a1-211">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="c87a1-212">Örnek 2: "fileFilter": 2014 - 1-? txt"</span><span class="sxs-lookup"><span data-stu-id="c87a1-212">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="c87a1-213">Bu fileFilter bir giriş FileShare veri kümesi için geçerli olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c87a1-213">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="c87a1-214">Hayır</span><span class="sxs-lookup"><span data-stu-id="c87a1-214">No</span></span> |
| <span data-ttu-id="c87a1-215">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="c87a1-215">partitionedBy</span></span> |<span data-ttu-id="c87a1-216">Zaman serisi veri partitionedBy toospecify dinamik folderPath/fileName kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c87a1-216">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="c87a1-217">İçin verileri saatte parametreli folderPath örneğidir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-217">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="c87a1-218">Hayır</span><span class="sxs-lookup"><span data-stu-id="c87a1-218">No</span></span> |
| <span data-ttu-id="c87a1-219">Biçimi</span><span class="sxs-lookup"><span data-stu-id="c87a1-219">format</span></span> | <span data-ttu-id="c87a1-220">şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="c87a1-220">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="c87a1-221">Set hello **türü** biçimi tooone şu değerlerden biri altında özellik.</span><span class="sxs-lookup"><span data-stu-id="c87a1-221">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="c87a1-222">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="c87a1-222">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="c87a1-223">Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="c87a1-223">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="c87a1-224">Hayır</span><span class="sxs-lookup"><span data-stu-id="c87a1-224">No</span></span> |
| <span data-ttu-id="c87a1-225">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="c87a1-225">compression</span></span> | <span data-ttu-id="c87a1-226">Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin.</span><span class="sxs-lookup"><span data-stu-id="c87a1-226">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="c87a1-227">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="c87a1-227">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="c87a1-228">Desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="c87a1-228">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="c87a1-229">bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="c87a1-229">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="c87a1-230">Hayır</span><span class="sxs-lookup"><span data-stu-id="c87a1-230">No</span></span> |

> [!NOTE]
> <span data-ttu-id="c87a1-231">Dosya adı ve fileFilter aynı anda kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="c87a1-231">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="c87a1-232">PartitionedBy özelliğini kullanma</span><span class="sxs-lookup"><span data-stu-id="c87a1-232">Using partitionedBy property</span></span>
<span data-ttu-id="c87a1-233">Merhaba önceki bölümünde belirtildiği gibi bir dinamik folderPath ve zaman serisi verileri için dosya adı ile Merhaba belirtebilirsiniz **partitionedBy** özelliği, [Data Factory işlevler ve hello sistem değişkenleri](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="c87a1-233">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="c87a1-234">toounderstand zaman serisi veri kümeleri, zamanlama ve dilimleri hakkında daha fazla ayrıntı görmek [veri kümeleri oluşturma](data-factory-create-datasets.md), [zamanlama ve yürütme](data-factory-scheduling-and-execution.md), ve [ardışık düzen oluşturma](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="c87a1-234">toounderstand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="c87a1-235">Örnek 1:</span><span class="sxs-lookup"><span data-stu-id="c87a1-235">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="c87a1-236">Bu örnekte, {dilim} hello değişkeninin değeri hello Data Factory sistem SliceStart hello biçiminde (YYYYMMDDHH) ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-236">In this example, {Slice} is replaced with hello value of hello Data Factory system variable SliceStart in hello format (YYYYMMDDHH).</span></span> <span data-ttu-id="c87a1-237">SliceStart toostart süresi hello dilimin başvurur.</span><span class="sxs-lookup"><span data-stu-id="c87a1-237">SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="c87a1-238">Merhaba folderPath her dilim için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="c87a1-238">hello folderPath is different for each slice.</span></span> <span data-ttu-id="c87a1-239">Örneğin: wikidatagateway/wikisampledataout/2014100103 veya wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="c87a1-239">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="c87a1-240">Örnek 2:</span><span class="sxs-lookup"><span data-stu-id="c87a1-240">Sample 2:</span></span>

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

<span data-ttu-id="c87a1-241">Bu örnekte, yıl, ay, gün ve saat SliceStart hello folderPath ve dosya adı özellikleri kullanan ayrı değişkenlere ayıklanır.</span><span class="sxs-lookup"><span data-stu-id="c87a1-241">In this example, year, month, day, and time of SliceStart are extracted into separate variables that hello folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="c87a1-242">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="c87a1-242">Copy activity properties</span></span>
<span data-ttu-id="c87a1-243">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c87a1-243">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c87a1-244">Ad, açıklama, giriş ve çıkış veri kümeleri ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-244">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="c87a1-245">Oysa hello kullanılabilen özellikleri **typeProperties** hello etkinlik bölümünü her etkinlik türü ile değişir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-245">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span>

<span data-ttu-id="c87a1-246">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-246">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="c87a1-247">Bir şirket içi dosya sisteminden veri taşıyorsanız, hello kaynak türü hello kopyalama etkinliği çok ayarladığınız**FileSystemSource**.</span><span class="sxs-lookup"><span data-stu-id="c87a1-247">If you are moving data from an on-premises file system, you set hello source type in hello copy activity too**FileSystemSource**.</span></span> <span data-ttu-id="c87a1-248">Benzer şekilde, veri tooan taşıyorsanız, şirket içi dosya sistemi, hello Havuz türü hello kopyalama etkinliği çok ayarladığınız**FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="c87a1-248">Similarly, if you are moving data tooan on-premises file system, you set hello sink type in hello copy activity too**FileSystemSink**.</span></span> <span data-ttu-id="c87a1-249">Bu bölümde FileSystemSource ve FileSystemSink tarafından desteklenen özellikler listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="c87a1-249">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="c87a1-250">**FileSystemSource** aşağıdaki özelliklere hello destekler:</span><span class="sxs-lookup"><span data-stu-id="c87a1-250">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="c87a1-251">Özellik</span><span class="sxs-lookup"><span data-stu-id="c87a1-251">Property</span></span> | <span data-ttu-id="c87a1-252">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c87a1-252">Description</span></span> | <span data-ttu-id="c87a1-253">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="c87a1-253">Allowed values</span></span> | <span data-ttu-id="c87a1-254">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c87a1-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c87a1-255">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="c87a1-255">recursive</span></span> |<span data-ttu-id="c87a1-256">Merhaba klasörlerdeki veya yalnızca klasörden hello belirtilen Hello veri yinelemeli olarak okunur olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-256">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="c87a1-257">TRUE, False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="c87a1-257">True, False (default)</span></span> |<span data-ttu-id="c87a1-258">Hayır</span><span class="sxs-lookup"><span data-stu-id="c87a1-258">No</span></span> |

<span data-ttu-id="c87a1-259">**FileSystemSink** aşağıdaki özelliklere hello destekler:</span><span class="sxs-lookup"><span data-stu-id="c87a1-259">**FileSystemSink** supports hello following properties:</span></span>

| <span data-ttu-id="c87a1-260">Özellik</span><span class="sxs-lookup"><span data-stu-id="c87a1-260">Property</span></span> | <span data-ttu-id="c87a1-261">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c87a1-261">Description</span></span> | <span data-ttu-id="c87a1-262">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="c87a1-262">Allowed values</span></span> | <span data-ttu-id="c87a1-263">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c87a1-263">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c87a1-264">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="c87a1-264">copyBehavior</span></span> |<span data-ttu-id="c87a1-265">Merhaba kaynağı BlobSource veya dosya sistemi olduğunda hello kopyalama davranışını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c87a1-265">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="c87a1-266">**PreserveHierarchy:** hello dosya hiyerarşisi hello hedef klasörde korur.</span><span class="sxs-lookup"><span data-stu-id="c87a1-266">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="c87a1-267">Diğer bir deyişle, hello kaynak dosya toohello kaynak klasörün hello göreli yol olduğundan hello hello hedef dosya toohello hedef klasörü hello göreli yolu ile aynı.</span><span class="sxs-lookup"><span data-stu-id="c87a1-267">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="c87a1-268">**FlattenHierarchy:** hello kaynak klasördeki tüm dosyaları hedef klasörün hello ilk düzeyi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c87a1-268">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="c87a1-269">Merhaba hedef dosyaları otomatik olarak oluşturulur adıyla oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c87a1-269">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="c87a1-270">**MergeFiles:** hello kaynak klasör tooone dosyasından tüm dosyaları birleştirir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-270">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="c87a1-271">Merhaba dosya adı/blob adı belirtilirse, hello belirtilen ad hello birleştirilmiş dosya adı değil.</span><span class="sxs-lookup"><span data-stu-id="c87a1-271">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="c87a1-272">Aksi halde, bir otomatik olarak oluşturulan dosya adı değil.</span><span class="sxs-lookup"><span data-stu-id="c87a1-272">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="c87a1-273">Hayır</span><span class="sxs-lookup"><span data-stu-id="c87a1-273">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="c87a1-274">özyinelemeli ve copyBehavior örnekleri</span><span class="sxs-lookup"><span data-stu-id="c87a1-274">recursive and copyBehavior examples</span></span>
<span data-ttu-id="c87a1-275">Bu bölümde hello kopyalama işlemi farklı birleşimlerini hello özyinelemeli ve copyBehavior özelliklerine ilişkin değerleri için sonuçta elde edilen davranışını hello açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c87a1-275">This section describes hello resulting behavior of hello Copy operation for different combinations of values for hello recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="c87a1-276">özyinelemeli değeri</span><span class="sxs-lookup"><span data-stu-id="c87a1-276">recursive value</span></span> | <span data-ttu-id="c87a1-277">copyBehavior değeri</span><span class="sxs-lookup"><span data-stu-id="c87a1-277">copyBehavior value</span></span> | <span data-ttu-id="c87a1-278">Bunun sonucunda oluşan davranışı</span><span class="sxs-lookup"><span data-stu-id="c87a1-278">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c87a1-279">TRUE</span><span class="sxs-lookup"><span data-stu-id="c87a1-279">true</span></span> |<span data-ttu-id="c87a1-280">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="c87a1-280">preserveHierarchy</span></span> |<span data-ttu-id="c87a1-281">Kaynak klasör Klasör1 yapı izlenerek hello ile</span><span class="sxs-lookup"><span data-stu-id="c87a1-281">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="c87a1-282">Klasör1</span><span class="sxs-lookup"><span data-stu-id="c87a1-282">Folder1</span></span><br/><span data-ttu-id="c87a1-283">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="c87a1-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c87a1-284">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="c87a1-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c87a1-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c87a1-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c87a1-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="c87a1-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c87a1-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c87a1-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c87a1-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c87a1-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c87a1-289">Merhaba hedef klasör Klasör1 aynı hello kaynağı olarak yapısı hello oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="c87a1-289">hello target folder Folder1 is created with hello same structure as hello source:</span></span><br/><br/><span data-ttu-id="c87a1-290">Klasör1</span><span class="sxs-lookup"><span data-stu-id="c87a1-290">Folder1</span></span><br/><span data-ttu-id="c87a1-291">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="c87a1-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c87a1-292">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="c87a1-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c87a1-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c87a1-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c87a1-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="c87a1-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c87a1-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c87a1-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c87a1-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c87a1-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="c87a1-297">TRUE</span><span class="sxs-lookup"><span data-stu-id="c87a1-297">true</span></span> |<span data-ttu-id="c87a1-298">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="c87a1-298">flattenHierarchy</span></span> |<span data-ttu-id="c87a1-299">Kaynak klasör Klasör1 yapı izlenerek hello ile</span><span class="sxs-lookup"><span data-stu-id="c87a1-299">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="c87a1-300">Klasör1</span><span class="sxs-lookup"><span data-stu-id="c87a1-300">Folder1</span></span><br/><span data-ttu-id="c87a1-301">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="c87a1-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c87a1-302">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="c87a1-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c87a1-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c87a1-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c87a1-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="c87a1-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c87a1-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c87a1-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c87a1-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c87a1-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c87a1-307">Merhaba hedef Klasör1 yapı izlenerek hello ile oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="c87a1-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="c87a1-308">Klasör1</span><span class="sxs-lookup"><span data-stu-id="c87a1-308">Folder1</span></span><br/><span data-ttu-id="c87a1-309">&nbsp;&nbsp;&nbsp;&nbsp;dosya1 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="c87a1-309">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="c87a1-310">&nbsp;&nbsp;&nbsp;&nbsp;dosya2 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="c87a1-310">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="c87a1-311">&nbsp;&nbsp;&nbsp;&nbsp;dosya3 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="c87a1-311">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="c87a1-312">&nbsp;&nbsp;&nbsp;&nbsp;File4 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="c87a1-312">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="c87a1-313">&nbsp;&nbsp;&nbsp;&nbsp;File5 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="c87a1-313">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="c87a1-314">TRUE</span><span class="sxs-lookup"><span data-stu-id="c87a1-314">true</span></span> |<span data-ttu-id="c87a1-315">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="c87a1-315">mergeFiles</span></span> |<span data-ttu-id="c87a1-316">Kaynak klasör Klasör1 yapı izlenerek hello ile</span><span class="sxs-lookup"><span data-stu-id="c87a1-316">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="c87a1-317">Klasör1</span><span class="sxs-lookup"><span data-stu-id="c87a1-317">Folder1</span></span><br/><span data-ttu-id="c87a1-318">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="c87a1-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c87a1-319">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="c87a1-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c87a1-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c87a1-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c87a1-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="c87a1-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c87a1-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c87a1-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c87a1-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c87a1-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c87a1-324">Merhaba hedef Klasör1 yapı izlenerek hello ile oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="c87a1-324">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="c87a1-325">Klasör1</span><span class="sxs-lookup"><span data-stu-id="c87a1-325">Folder1</span></span><br/><span data-ttu-id="c87a1-326">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1 + dosya2 + dosya3 + File4 + 5 dosyası içeriği otomatik olarak oluşturulan dosya adına sahip bir dosya halinde birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="c87a1-327">False</span><span class="sxs-lookup"><span data-stu-id="c87a1-327">false</span></span> |<span data-ttu-id="c87a1-328">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="c87a1-328">preserveHierarchy</span></span> |<span data-ttu-id="c87a1-329">Kaynak klasör Klasör1 yapı izlenerek hello ile</span><span class="sxs-lookup"><span data-stu-id="c87a1-329">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="c87a1-330">Klasör1</span><span class="sxs-lookup"><span data-stu-id="c87a1-330">Folder1</span></span><br/><span data-ttu-id="c87a1-331">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="c87a1-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c87a1-332">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="c87a1-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c87a1-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c87a1-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c87a1-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="c87a1-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c87a1-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c87a1-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c87a1-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c87a1-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c87a1-337">Merhaba hedef klasör Klasör1 yapı izlenerek hello ile oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="c87a1-337">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="c87a1-338">Klasör1</span><span class="sxs-lookup"><span data-stu-id="c87a1-338">Folder1</span></span><br/><span data-ttu-id="c87a1-339">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="c87a1-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c87a1-340">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="c87a1-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="c87a1-341">Dosya3, File4 ve File5 Subfolder1 toplanma değil.</span><span class="sxs-lookup"><span data-stu-id="c87a1-341">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="c87a1-342">False</span><span class="sxs-lookup"><span data-stu-id="c87a1-342">false</span></span> |<span data-ttu-id="c87a1-343">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="c87a1-343">flattenHierarchy</span></span> |<span data-ttu-id="c87a1-344">Kaynak klasör Klasör1 yapı izlenerek hello ile</span><span class="sxs-lookup"><span data-stu-id="c87a1-344">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="c87a1-345">Klasör1</span><span class="sxs-lookup"><span data-stu-id="c87a1-345">Folder1</span></span><br/><span data-ttu-id="c87a1-346">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="c87a1-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c87a1-347">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="c87a1-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c87a1-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c87a1-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c87a1-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="c87a1-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c87a1-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c87a1-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c87a1-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c87a1-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c87a1-352">Merhaba hedef klasör Klasör1 yapı izlenerek hello ile oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="c87a1-352">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="c87a1-353">Klasör1</span><span class="sxs-lookup"><span data-stu-id="c87a1-353">Folder1</span></span><br/><span data-ttu-id="c87a1-354">&nbsp;&nbsp;&nbsp;&nbsp;dosya1 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="c87a1-354">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="c87a1-355">&nbsp;&nbsp;&nbsp;&nbsp;dosya2 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="c87a1-355">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="c87a1-356">Dosya3, File4 ve File5 Subfolder1 toplanma değil.</span><span class="sxs-lookup"><span data-stu-id="c87a1-356">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="c87a1-357">False</span><span class="sxs-lookup"><span data-stu-id="c87a1-357">false</span></span> |<span data-ttu-id="c87a1-358">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="c87a1-358">mergeFiles</span></span> |<span data-ttu-id="c87a1-359">Kaynak klasör Klasör1 yapı izlenerek hello ile</span><span class="sxs-lookup"><span data-stu-id="c87a1-359">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="c87a1-360">Klasör1</span><span class="sxs-lookup"><span data-stu-id="c87a1-360">Folder1</span></span><br/><span data-ttu-id="c87a1-361">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1</span><span class="sxs-lookup"><span data-stu-id="c87a1-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c87a1-362">&nbsp;&nbsp;&nbsp;&nbsp;Dosya2</span><span class="sxs-lookup"><span data-stu-id="c87a1-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c87a1-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c87a1-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c87a1-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Dosya3</span><span class="sxs-lookup"><span data-stu-id="c87a1-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c87a1-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c87a1-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c87a1-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c87a1-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c87a1-367">Merhaba hedef klasör Klasör1 yapı izlenerek hello ile oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="c87a1-367">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="c87a1-368">Klasör1</span><span class="sxs-lookup"><span data-stu-id="c87a1-368">Folder1</span></span><br/><span data-ttu-id="c87a1-369">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1 + dosya2 içeriği otomatik olarak oluşturulan dosya adına sahip bir dosya halinde birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="c87a1-370">&nbsp;&nbsp;&nbsp;&nbsp;Dosya1 için otomatik olarak oluşturulan adı</span><span class="sxs-lookup"><span data-stu-id="c87a1-370">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="c87a1-371">Dosya3, File4 ve File5 Subfolder1 toplanma değil.</span><span class="sxs-lookup"><span data-stu-id="c87a1-371">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="c87a1-372">Desteklenen dosya ve sıkıştırma biçimleri</span><span class="sxs-lookup"><span data-stu-id="c87a1-372">Supported file and compression formats</span></span>
<span data-ttu-id="c87a1-373">Bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md) makale ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="c87a1-373">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a><span data-ttu-id="c87a1-374">Veri tooand dosya sisteminden kopyalama için JSON örnekleri</span><span class="sxs-lookup"><span data-stu-id="c87a1-374">JSON examples for copying data tooand from file system</span></span>
<span data-ttu-id="c87a1-375">Merhaba aşağıdaki örneklerde sağlayan örnek JSON tanımları toocreate bir ardışık düzen hello kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c87a1-375">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c87a1-376">Bunlar Göster nasıl toocopy veri tooand bir şirket içi dosya sistemi ve Azure Blob Depolama.</span><span class="sxs-lookup"><span data-stu-id="c87a1-376">They show how toocopy data tooand from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="c87a1-377">Ancak, veri kopyalayabilirsiniz *doğrudan* herhangi birinden hello kaynakları tooany listelenen hello havuzlarını, [desteklenen kaynakları ve havuzlarını](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kopya etkinliği Azure Data Factory kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c87a1-377">However, you can copy data *directly* from any of hello sources tooany of hello sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a><span data-ttu-id="c87a1-378">Örnek: bir şirket içi dosya sistemi tooAzure Blob depolama alanına veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="c87a1-378">Example: Copy data from an on-premises file system tooAzure Blob storage</span></span>
<span data-ttu-id="c87a1-379">Bu örnek göstermektedir nasıl bir şirket içi dosya sistemi tooAzure Blob Depolama toocopy verileri.</span><span class="sxs-lookup"><span data-stu-id="c87a1-379">This sample shows how toocopy data from an on-premises file system tooAzure Blob storage.</span></span> <span data-ttu-id="c87a1-380">Merhaba örnek Data Factory varlıklarını aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="c87a1-380">hello sample has hello following Data Factory entities:</span></span>

* <span data-ttu-id="c87a1-381">Bağlı hizmet türü [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c87a1-381">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="c87a1-382">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c87a1-382">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="c87a1-383">Bir giriş [dataset](data-factory-create-datasets.md) türü [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c87a1-383">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="c87a1-384">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c87a1-384">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="c87a1-385">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [FileSystemSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c87a1-385">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c87a1-386">Aşağıdaki örnek hello time series verilerini her saat bir şirket içi dosya sistemi tooAzure Blob Depolama kopyalar.</span><span class="sxs-lookup"><span data-stu-id="c87a1-386">hello following sample copies time-series data from an on-premises file system tooAzure Blob storage every hour.</span></span> <span data-ttu-id="c87a1-387">Bu örnekler kullanılan JSON özellikleri hello hello örnekleri sonra hello bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c87a1-387">hello JSON properties that are used in these samples are described in hello sections after hello samples.</span></span>

<span data-ttu-id="c87a1-388">İlk adım olarak, veri yönetimi ağ geçidi kurun hello yönergelerini uygun şekilde ayarlayın. [şirket içi kaynakları ve veri yönetimi ağ geçidi ile Merhaba bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="c87a1-388">As a first step, set up Data Management Gateway as per hello instructions in [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="c87a1-389">**Şirket içi dosya sunucusu hizmeti bağlı:**</span><span class="sxs-lookup"><span data-stu-id="c87a1-389">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="c87a1-390">Merhaba kullanmanızı öneririz **encryptedCredential** özelliği yerine hello **UserID** ve **parola** özellikleri.</span><span class="sxs-lookup"><span data-stu-id="c87a1-390">We recommend using hello **encryptedCredential** property instead hello **userid** and **password** properties.</span></span> <span data-ttu-id="c87a1-391">Bkz: [dosya sunucusuna bağlı hizmetinin](#linked-service-properties) bu hakkındaki ayrıntılar için bağlantılı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="c87a1-391">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="c87a1-392">**Azure Storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="c87a1-392">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="c87a1-393">**Şirket içi sistem girdi veri kümesi dosya:**</span><span class="sxs-lookup"><span data-stu-id="c87a1-393">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="c87a1-394">Verileri yeni bir dosyadan saatte kayıt.</span><span class="sxs-lookup"><span data-stu-id="c87a1-394">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="c87a1-395">folderPath hello ve fileName özellikleri hello dilimin hello başlangıç zamanı temel alınarak belirlenir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-395">hello folderPath and fileName properties are determined based on hello start time of hello slice.</span></span>  

<span data-ttu-id="c87a1-396">Ayar `"external": "true"` bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil veri fabrikası bildirir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-396">Setting `"external": "true"` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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

<span data-ttu-id="c87a1-397">**Azure Blob Depolama çıktı veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="c87a1-397">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="c87a1-398">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="c87a1-398">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="c87a1-399">hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-399">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="c87a1-400">Merhaba klasör yolu hello yıl, ay, gün ve saat bölümlerini hello başlangıç saatini kullanır.</span><span class="sxs-lookup"><span data-stu-id="c87a1-400">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="c87a1-401">**Dosya sistemi kaynak ve Blob havuz sahip işlem hattı kopyalama etkinliğinde:**</span><span class="sxs-lookup"><span data-stu-id="c87a1-401">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="c87a1-402">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-402">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="c87a1-403">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**FileSystemSource**, ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c87a1-403">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "FileSystemSource"
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

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a><span data-ttu-id="c87a1-404">Örnek: verileri Azure SQL veritabanı tooan şirket içi dosya sisteminden kopyalama</span><span class="sxs-lookup"><span data-stu-id="c87a1-404">Example: Copy data from Azure SQL Database tooan on-premises file system</span></span>
<span data-ttu-id="c87a1-405">Merhaba, aşağıdaki örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="c87a1-405">hello following sample shows:</span></span>

* <span data-ttu-id="c87a1-406">Bağlı hizmet türü [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="c87a1-406">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="c87a1-407">Bağlı hizmet türü [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c87a1-407">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="c87a1-408">Bir giriş veri kümesi türü [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c87a1-408">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="c87a1-409">Bir çıkış veri kümesi türü [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c87a1-409">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="c87a1-410">Kullanan kopyalama etkinliği ile işlem hattı [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) ve [FileSystemSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c87a1-410">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="c87a1-411">Merhaba örnek time series verilerini her saat bir Azure SQL tablosu tooan şirket içi dosya sisteminden kopyalar.</span><span class="sxs-lookup"><span data-stu-id="c87a1-411">hello sample copies time-series data from an Azure SQL table tooan on-premises file system every hour.</span></span> <span data-ttu-id="c87a1-412">Bu örnekler kullanılan JSON özellikleri hello hello örnekleri sonra bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c87a1-412">hello JSON properties that are used in these samples are described in sections after hello samples.</span></span>

<span data-ttu-id="c87a1-413">**Azure SQL Database hizmeti bağlı:**</span><span class="sxs-lookup"><span data-stu-id="c87a1-413">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```

<span data-ttu-id="c87a1-414">**Şirket içi dosya sunucusu hizmeti bağlı:**</span><span class="sxs-lookup"><span data-stu-id="c87a1-414">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="c87a1-415">Merhaba kullanmanızı öneririz **encryptedCredential** hello yerine özelliği **UserID** ve **parola** özellikleri.</span><span class="sxs-lookup"><span data-stu-id="c87a1-415">We recommend using hello **encryptedCredential** property instead of using hello **userid** and **password** properties.</span></span> <span data-ttu-id="c87a1-416">Bkz: [dosya sistemi bağlantılı hizmet](#linked-service-properties) bu hakkındaki ayrıntılar için bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="c87a1-416">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="c87a1-417">**Azure SQL girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="c87a1-417">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="c87a1-418">Merhaba örnek bir tablo "MyTable" Azure SQL oluşturduğunuz ve için zaman serisi veri "timestampcolumn" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="c87a1-418">hello sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="c87a1-419">Ayar ``“external”: ”true”`` bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil veri fabrikası bildirir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-419">Setting ``“external”: ”true”`` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
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

<span data-ttu-id="c87a1-420">**Şirket içi sistem çıktı veri kümesi dosya:**</span><span class="sxs-lookup"><span data-stu-id="c87a1-420">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="c87a1-421">Veri kopyalanan tooa yeni saatte dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="c87a1-421">Data is copied tooa new file every hour.</span></span> <span data-ttu-id="c87a1-422">Merhaba folderPath ve hello blob fileName hello dilimin hello başlangıç zamanı temel alınarak belirlenir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-422">hello folderPath and fileName for hello blob are determined based on hello start time of hello slice.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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

<span data-ttu-id="c87a1-423">**SQL kaynak ve dosya sistemi havuz sahip işlem hattı kopyalama etkinliğinde:**</span><span class="sxs-lookup"><span data-stu-id="c87a1-423">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="c87a1-424">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="c87a1-424">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="c87a1-425">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**SqlSource**ve hello **havuz** türü olarak ayarlanmış çok**FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="c87a1-425">In hello pipeline JSON definition, hello **source** type is set too**SqlSource**, and hello **sink** type is set too**FileSystemSink**.</span></span> <span data-ttu-id="c87a1-426">Merhaba belirtilen hello SQL sorgusu **SqlReaderQuery** özelliği saat toocopy geçmiş hello hello veri seçer.</span><span class="sxs-lookup"><span data-stu-id="c87a1-426">hello SQL query that is specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


<span data-ttu-id="c87a1-427">Ayrıca, kaynak veri kümesi toocolumns hello kopyalama etkinliği tanımında havuz kümesinden sütunlarından eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c87a1-427">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="c87a1-428">Ayrıntılar için bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c87a1-428">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c87a1-429">Performans ve ayar</span><span class="sxs-lookup"><span data-stu-id="c87a1-429">Performance and tuning</span></span>
 <span data-ttu-id="c87a1-430">anahtarı hakkında toolearn Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi hello performansını, hello bkz [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="c87a1-430">toolearn about key factors that impact hello performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
