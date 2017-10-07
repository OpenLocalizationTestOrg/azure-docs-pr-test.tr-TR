---
title: "Şirket içi HDFS aaaMove verilerden | Microsoft Docs"
description: "Nasıl toomove verileri HDFS Azure Data Factory kullanarak şirket içi hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a><span data-ttu-id="1bb2b-103">Azure Data Factory kullanarak şirket içi HDFS taşıma verileri</span><span class="sxs-lookup"><span data-stu-id="1bb2b-103">Move data from on-premises HDFS using Azure Data Factory</span></span>
<span data-ttu-id="1bb2b-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove verileri bir şirket içi HDFS de açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises HDFS.</span></span> <span data-ttu-id="1bb2b-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="1bb2b-106">Verileri HDFS desteklenen tooany havuz veri deposundan kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-106">You can copy data from HDFS tooany supported sink data store.</span></span> <span data-ttu-id="1bb2b-107">Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="1bb2b-108">Veri Fabrikası şu anda bir şirket içi HDFS tooother veri depolarına yalnızca taşıma verilerden destekler, ancak verileri diğer veriler taşıma değil için depoları tooan HDFS şirket.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-108">Data factory currently supports only moving data from an on-premises HDFS tooother data stores, but not for moving data from other data stores tooan on-premises HDFS.</span></span>

> [!NOTE]
> <span data-ttu-id="1bb2b-109">Başarıyla kopyalanan toohello hedef tamamlandıktan sonra kopyalama etkinliği hello kaynak dosyayı silmez.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="1bb2b-110">Sonra başarılı bir kopyasını toodelete hello kaynak dosyası gerekiyorsa, bir özel etkinlik toodelete hello dosyası oluşturun ve hello ardışık düzeninde hello etkinliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="1bb2b-111">Bağlantıyı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="1bb2b-111">Enabling connectivity</span></span>
<span data-ttu-id="1bb2b-112">Data Factory Hizmeti'ne hello veri yönetimi ağ geçidi kullanarak bağlanan tooon içi HDFS destekler.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-112">Data Factory service supports connecting tooon-premises HDFS using hello Data Management Gateway.</span></span> <span data-ttu-id="1bb2b-113">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale toolearn veri yönetimi ağ geçidi ve hello ağ geçidi kurun ayarlama hakkında adım adım yönergeleri hakkında.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-113">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="1bb2b-114">Bir Azure Iaas sanal barındırılan olsa bile hello ağ geçidi tooconnect tooHDFS kullanın.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-114">Use hello gateway tooconnect tooHDFS even if it is hosted in an Azure IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="1bb2b-115">Veri Yönetimi ağ geçidi çok erişebilir yapma emin hello**tüm** hello [ad düğümü sunucusu]: [name düğümü bağlantı noktası] ve [veri düğümü sunucuları]: [veri düğümü bağlantı noktası] hello Hadoop kümesi.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-115">Make sure hello Data Management Gateway can access too**ALL** hello [name node server]:[name node port] and [data node servers]:[data node port] of hello Hadoop cluster.</span></span> <span data-ttu-id="1bb2b-116">[Adı düğümü bağlantı noktası] 50070 varsayılandır ve [veri düğümü bağlantı noktası] 50075 varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-116">Default [name node port] is 50070, and default [data node port] is 50075.</span></span>

<span data-ttu-id="1bb2b-117">Ağ geçidi üzerinde hello yükleyebilirsiniz sırasında aynı makine ya da hello Azure VM HDFS hello gibi şirket içi, bir ayrı makine/Azure Iaas VM hello ağ geçidi yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-117">While you can install gateway on hello same on-premises machine or hello Azure VM as hello HDFS, we recommend that you install hello gateway on a separate machine/Azure IaaS VM.</span></span> <span data-ttu-id="1bb2b-118">Ağ geçidi ayrı bir makinede sahip kaynak çekişmesini azaltır ve performansı artırır.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-118">Having gateway on a separate machine reduces resource contention and improves performance.</span></span> <span data-ttu-id="1bb2b-119">Merhaba ağ geçidi ayrı bir makineye yüklediğinizde hello makine mümkün tooaccess hello hello HDFS makineyle olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-119">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello HDFS.</span></span>

## <a name="getting-started"></a><span data-ttu-id="1bb2b-120">Başlarken</span><span class="sxs-lookup"><span data-stu-id="1bb2b-120">Getting started</span></span>
<span data-ttu-id="1bb2b-121">Farklı araçlar/API'lerini kullanarak verileri HDFS kaynağından taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-121">You can create a pipeline with a copy activity that moves data from a HDFS source by using different tools/APIs.</span></span>

<span data-ttu-id="1bb2b-122">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="1bb2b-123">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="1bb2b-124">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="1bb2b-125">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="1bb2b-126">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="1bb2b-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="1bb2b-127">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="1bb2b-128">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="1bb2b-129">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="1bb2b-130">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="1bb2b-131">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="1bb2b-132">HDFS veri deposundan kullanılan toocopy verileri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: şirket içi HDFS tooAzure Blob veri kopyalama](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a HDFS data store, see [JSON example: Copy data from on-premises HDFS tooAzure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section of this article.</span></span>

<span data-ttu-id="1bb2b-133">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooHDFS olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="1bb2b-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooHDFS:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="1bb2b-134">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="1bb2b-134">Linked service properties</span></span>
<span data-ttu-id="1bb2b-135">Bağlı hizmet, bir veri deposu tooa veri fabrikası bağlar.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-135">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="1bb2b-136">Bağlı hizmet türü oluşturma **Hdfs** toolink bir şirket içi HDFS tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-136">You create a linked service of type **Hdfs** toolink an on-premises HDFS tooyour data factory.</span></span> <span data-ttu-id="1bb2b-137">Aşağıdaki tablonun hello JSON öğeleri belirli tooHDFS bağlantılı hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-137">hello following table provides description for JSON elements specific tooHDFS linked service.</span></span>

| <span data-ttu-id="1bb2b-138">Özellik</span><span class="sxs-lookup"><span data-stu-id="1bb2b-138">Property</span></span> | <span data-ttu-id="1bb2b-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1bb2b-139">Description</span></span> | <span data-ttu-id="1bb2b-140">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1bb2b-140">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1bb2b-141">type</span><span class="sxs-lookup"><span data-stu-id="1bb2b-141">type</span></span> |<span data-ttu-id="1bb2b-142">Merhaba type özelliği ayarlanmalıdır: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="1bb2b-142">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="1bb2b-143">Evet</span><span class="sxs-lookup"><span data-stu-id="1bb2b-143">Yes</span></span> |
| <span data-ttu-id="1bb2b-144">Url</span><span class="sxs-lookup"><span data-stu-id="1bb2b-144">Url</span></span> |<span data-ttu-id="1bb2b-145">URL toohello HDFS</span><span class="sxs-lookup"><span data-stu-id="1bb2b-145">URL toohello HDFS</span></span> |<span data-ttu-id="1bb2b-146">Evet</span><span class="sxs-lookup"><span data-stu-id="1bb2b-146">Yes</span></span> |
| <span data-ttu-id="1bb2b-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="1bb2b-147">authenticationType</span></span> |<span data-ttu-id="1bb2b-148">Anonim veya Windows.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-148">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="1bb2b-149">toouse **Kerberos kimlik doğrulaması** HDFS bağlayıcı için çok başvuran[Bu bölümde](#use-kerberos-authentication-for-hdfs-connector) tooset şirket içi ortamınızı uygun şekilde.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-149">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="1bb2b-150">Evet</span><span class="sxs-lookup"><span data-stu-id="1bb2b-150">Yes</span></span> |
| <span data-ttu-id="1bb2b-151">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="1bb2b-151">userName</span></span> |<span data-ttu-id="1bb2b-152">Kullanıcı adı için Windows kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-152">Username for Windows authentication.</span></span> |<span data-ttu-id="1bb2b-153">Evet (Windows kimlik doğrulaması için)</span><span class="sxs-lookup"><span data-stu-id="1bb2b-153">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="1bb2b-154">password</span><span class="sxs-lookup"><span data-stu-id="1bb2b-154">password</span></span> |<span data-ttu-id="1bb2b-155">Windows kimlik doğrulaması için parola.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-155">Password for Windows authentication.</span></span> |<span data-ttu-id="1bb2b-156">Evet (Windows kimlik doğrulaması için)</span><span class="sxs-lookup"><span data-stu-id="1bb2b-156">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="1bb2b-157">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1bb2b-157">gatewayName</span></span> |<span data-ttu-id="1bb2b-158">Data Factory hizmetinin hello hello ağ geçidinin adı tooconnect toohello HDFS kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-158">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="1bb2b-159">Evet</span><span class="sxs-lookup"><span data-stu-id="1bb2b-159">Yes</span></span> |
| <span data-ttu-id="1bb2b-160">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="1bb2b-160">encryptedCredential</span></span> |<span data-ttu-id="1bb2b-161">[AzureRMDataFactoryEncryptValue yeni](https://msdn.microsoft.com/library/mt603802.aspx) hello erişim kimlik bilgisi çıktısı.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="1bb2b-162">Hayır</span><span class="sxs-lookup"><span data-stu-id="1bb2b-162">No</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="1bb2b-163">Anonim kimlik doğrulamasını kullanma</span><span class="sxs-lookup"><span data-stu-id="1bb2b-163">Using Anonymous authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a><span data-ttu-id="1bb2b-164">Windows kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="1bb2b-164">Using Windows authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a><span data-ttu-id="1bb2b-165">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="1bb2b-165">Dataset properties</span></span>
<span data-ttu-id="1bb2b-166">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="1bb2b-167">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="1bb2b-168">Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="1bb2b-169">Merhaba typeProperties bölüm türü veri kümesi için **FileShare** hello aşağıdaki özelliklere sahip (HDFS dataset içerir)</span><span class="sxs-lookup"><span data-stu-id="1bb2b-169">hello typeProperties section for dataset of type **FileShare** (which includes HDFS dataset) has hello following properties</span></span>

| <span data-ttu-id="1bb2b-170">Özellik</span><span class="sxs-lookup"><span data-stu-id="1bb2b-170">Property</span></span> | <span data-ttu-id="1bb2b-171">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1bb2b-171">Description</span></span> | <span data-ttu-id="1bb2b-172">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1bb2b-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1bb2b-173">folderPath</span><span class="sxs-lookup"><span data-stu-id="1bb2b-173">folderPath</span></span> |<span data-ttu-id="1bb2b-174">Yol toohello klasör.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-174">Path toohello folder.</span></span> <span data-ttu-id="1bb2b-175">Örnek:`myfolder`</span><span class="sxs-lookup"><span data-stu-id="1bb2b-175">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="1bb2b-176">Kaçış karakteri kullanmak ' \ ' hello dize özel karakter.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-176">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="1bb2b-177">Örneğin: folder\subfolder için klasör belirtin\\\\alt ve d:\samplefolder için d: belirtin\\\\ÖrnekKlasör.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-177">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="1bb2b-178">Bu özellik ile birleştirebilirsiniz **partitionBy** toohave klasör yolları dilimine göre başlangıç/bitiş tarih saatleri.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-178">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="1bb2b-179">Evet</span><span class="sxs-lookup"><span data-stu-id="1bb2b-179">Yes</span></span> |
| <span data-ttu-id="1bb2b-180">fileName</span><span class="sxs-lookup"><span data-stu-id="1bb2b-180">fileName</span></span> |<span data-ttu-id="1bb2b-181">Hello Hello hello dosyasının adını belirtin **folderPath** hello tablo toorefer tooa belirli dosya hello klasöründeki istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-181">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="1bb2b-182">Bu özellik için herhangi bir değer belirtmezseniz, hello tablo hello klasöründeki tooall dosyaları işaret eder.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-182">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="1bb2b-183">FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan hello dosyasının hello adı Bu biçim aşağıdaki hello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="1bb2b-183">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="1bb2b-184">Veriler. <Guid>.txt (örnek:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="1bb2b-184">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="1bb2b-185">Hayır</span><span class="sxs-lookup"><span data-stu-id="1bb2b-185">No</span></span> |
| <span data-ttu-id="1bb2b-186">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="1bb2b-186">partitionedBy</span></span> |<span data-ttu-id="1bb2b-187">partitionedBy kullanılan toospecify dinamik folderPath zaman serisi veri için dosya adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-187">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="1bb2b-188">Örnek: veri her saat için parametreli folderPath.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-188">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="1bb2b-189">Hayır</span><span class="sxs-lookup"><span data-stu-id="1bb2b-189">No</span></span> |
| <span data-ttu-id="1bb2b-190">Biçimi</span><span class="sxs-lookup"><span data-stu-id="1bb2b-190">format</span></span> | <span data-ttu-id="1bb2b-191">şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-191">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="1bb2b-192">Set hello **türü** biçimi tooone şu değerlerden biri altında özellik.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-192">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="1bb2b-193">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-193">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="1bb2b-194">Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-194">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="1bb2b-195">Hayır</span><span class="sxs-lookup"><span data-stu-id="1bb2b-195">No</span></span> |
| <span data-ttu-id="1bb2b-196">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="1bb2b-196">compression</span></span> | <span data-ttu-id="1bb2b-197">Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-197">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="1bb2b-198">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-198">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="1bb2b-199">Desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-199">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="1bb2b-200">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="1bb2b-200">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="1bb2b-201">Hayır</span><span class="sxs-lookup"><span data-stu-id="1bb2b-201">No</span></span> |

> [!NOTE]
> <span data-ttu-id="1bb2b-202">Dosya adı ve fileFilter aynı anda kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-202">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="1bb2b-203">PartionedBy özelliğini kullanma</span><span class="sxs-lookup"><span data-stu-id="1bb2b-203">Using partionedBy property</span></span>
<span data-ttu-id="1bb2b-204">Merhaba önceki bölümünde belirtildiği gibi bir dinamik folderPath ve zaman serisi verileri için dosya adı ile Merhaba belirtebilirsiniz **partitionedBy** özelliği, [Data Factory işlevler ve hello sistem değişkenleri](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="1bb2b-204">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="1bb2b-205">Zaman serisi veri kümeleri, zamanlama ve dilimleri hakkında daha fazla toolearn bkz [veri kümeleri oluşturma](data-factory-create-datasets.md), [zamanlama ve yürütme](data-factory-scheduling-and-execution.md), ve [oluşturma ardışık düzen](data-factory-create-pipelines.md) makaleleri.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-205">toolearn more about time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="1bb2b-206">Örnek 1:</span><span class="sxs-lookup"><span data-stu-id="1bb2b-206">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="1bb2b-207">Bu örnekte {dilim} belirtilen hello Data Factory sistem değişkenin değerini SliceStart hello biçiminde (YYYYMMDDHH) ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-207">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="1bb2b-208">Merhaba SliceStart hello dilim toostart süresini ifade eder.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-208">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="1bb2b-209">Merhaba folderPath her dilim için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-209">hello folderPath is different for each slice.</span></span> <span data-ttu-id="1bb2b-210">Örneğin: wikidatagateway/wikisampledataout/2014100103 veya wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-210">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="1bb2b-211">Örnek 2:</span><span class="sxs-lookup"><span data-stu-id="1bb2b-211">Sample 2:</span></span>

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
<span data-ttu-id="1bb2b-212">Bu örnekte, folderPath ve fileName özellikleri tarafından kullanılan ayrı değişkenleri içine yıl, ay, gün ve saat SliceStart ayıklanır.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-212">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="1bb2b-213">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="1bb2b-213">Copy activity properties</span></span>
<span data-ttu-id="1bb2b-214">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-214">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="1bb2b-215">Ad, açıklama, giriş ve çıkış tabloları ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-215">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="1bb2b-216">Oysa hello typeProperties bölümünde hello etkinlik özellikleri her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-216">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="1bb2b-217">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-217">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="1bb2b-218">Kopyalama kaynağı türü olduğunda etkinliği için **FileSystemSource** aşağıdaki özelliklere hello typeProperties bölümünde bulunur:</span><span class="sxs-lookup"><span data-stu-id="1bb2b-218">For Copy Activity, when source is of type **FileSystemSource** hello following properties are available in typeProperties section:</span></span>

<span data-ttu-id="1bb2b-219">**FileSystemSource** aşağıdaki özelliklere hello destekler:</span><span class="sxs-lookup"><span data-stu-id="1bb2b-219">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="1bb2b-220">Özellik</span><span class="sxs-lookup"><span data-stu-id="1bb2b-220">Property</span></span> | <span data-ttu-id="1bb2b-221">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1bb2b-221">Description</span></span> | <span data-ttu-id="1bb2b-222">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="1bb2b-222">Allowed values</span></span> | <span data-ttu-id="1bb2b-223">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1bb2b-223">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1bb2b-224">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="1bb2b-224">recursive</span></span> |<span data-ttu-id="1bb2b-225">Merhaba alt klasörler veya yalnızca hello belirtilen klasör Hello veri yinelemeli olarak okunur olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-225">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="1bb2b-226">TRUE, False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="1bb2b-226">True, False (default)</span></span> |<span data-ttu-id="1bb2b-227">Hayır</span><span class="sxs-lookup"><span data-stu-id="1bb2b-227">No</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="1bb2b-228">Desteklenen dosya ve sıkıştırma biçimleri</span><span class="sxs-lookup"><span data-stu-id="1bb2b-228">Supported file and compression formats</span></span>
<span data-ttu-id="1bb2b-229">Bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md) makale ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-229">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a><span data-ttu-id="1bb2b-230">JSON örnek: şirket içi HDFS tooAzure Blob veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="1bb2b-230">JSON example: Copy data from on-premises HDFS tooAzure Blob</span></span>
<span data-ttu-id="1bb2b-231">Bu örnek göstermektedir nasıl bir şirket içi HDFS tooAzure Blob Storage toocopy verileri.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-231">This sample shows how toocopy data from an on-premises HDFS tooAzure Blob Storage.</span></span> <span data-ttu-id="1bb2b-232">Ancak, veriler kopyalanabilir **doğrudan** belirtildiği hello havuzlarını tooany [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-232">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="1bb2b-233">Merhaba örnek Data Factory varlıklarını aşağıdaki hello için JSON tanımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-233">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="1bb2b-234">Bu tanımları toocreate bir ardışık düzen toocopy verileri HDFS tooAzure Blob Storage kullanarak kullanabileceğiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1bb2b-234">You can use these definitions toocreate a pipeline toocopy data from HDFS tooAzure Blob Storage by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

1. <span data-ttu-id="1bb2b-235">Bağlı hizmet türü [OnPremisesHdfs](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1bb2b-235">A linked service of type [OnPremisesHdfs](#linked-service-properties).</span></span>
2. <span data-ttu-id="1bb2b-236">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1bb2b-236">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="1bb2b-237">Bir giriş [dataset](data-factory-create-datasets.md) türü [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1bb2b-237">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
4. <span data-ttu-id="1bb2b-238">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1bb2b-238">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="1bb2b-239">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [FileSystemSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1bb2b-239">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="1bb2b-240">Merhaba örnek verileri saatte bir şirket içi HDFS tooan Azure blob kopyalar.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-240">hello sample copies data from an on-premises HDFS tooan Azure blob every hour.</span></span> <span data-ttu-id="1bb2b-241">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-241">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="1bb2b-242">İlk adım olarak, hello veri yönetimi ağ geçidi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-242">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="1bb2b-243">Merhaba hello'ndaki yönergeleri [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-243">hello instructions in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="1bb2b-244">**HDFS bağlantılı hizmeti:** kullandığı hello Windows kimlik doğrulaması Bu örnek.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-244">**HDFS linked service:** This example uses hello Windows authentication.</span></span> <span data-ttu-id="1bb2b-245">Bkz: [HDFS bağlantılı hizmeti](#linked-service-properties) bölümü için farklı tür kimlik doğrulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-245">See [HDFS linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="1bb2b-246">**Azure Storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="1bb2b-246">**Azure Storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="1bb2b-247">**HDFS giriş veri kümesi:** toohello HDFS klasörü DataTransfer/UnitTest bu veri kümesine başvuruyor /.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-247">**HDFS input dataset:** This dataset refers toohello HDFS folder DataTransfer/UnitTest/.</span></span> <span data-ttu-id="1bb2b-248">Hello ardışık tüm hello dosyalarını bu klasöre toohello hedef kopyalar.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-248">hello pipeline copies all hello files in this folder toohello destination.</span></span>

<span data-ttu-id="1bb2b-249">"Dış" ayarı: "true" bildirir hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-249">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

<span data-ttu-id="1bb2b-250">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="1bb2b-250">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="1bb2b-251">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="1bb2b-251">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="1bb2b-252">hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-252">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="1bb2b-253">Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-253">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="1bb2b-254">**Dosya sistemi kaynak ve Blob havuz sahip işlem hattı kopyalama etkinliğinde:**</span><span class="sxs-lookup"><span data-stu-id="1bb2b-254">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="1bb2b-255">Merhaba ardışık düzen içeren bir kopyalama etkinliği, yapılandırılmış toouse bu girdi ve çıktı veri kümeleri ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-255">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="1bb2b-256">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**FileSystemSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-256">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="1bb2b-257">Merhaba belirtilen hello SQL sorgusu **sorgu** özelliği saat toocopy geçmiş hello hello veri seçer.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-257">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a><span data-ttu-id="1bb2b-258">HDFS Bağlayıcısı için Kerberos kimlik doğrulamasını kullan</span><span class="sxs-lookup"><span data-stu-id="1bb2b-258">Use Kerberos authentication for HDFS connector</span></span>
<span data-ttu-id="1bb2b-259">HDFS Bağlayıcısı toouse Kerberos kimlik doğrulaması olarak şekilde hello şirket içi çevresi iki seçenekleri tooset vardır.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-259">There are two options tooset up hello on-premises environment so as toouse Kerberos Authentication in HDFS connector.</span></span> <span data-ttu-id="1bb2b-260">Merhaba bir durumunuz daha iyi uyduğunu seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-260">You can choose hello one better fits your case.</span></span>
* <span data-ttu-id="1bb2b-261">Seçenek 1: [birleştirme ağ geçidi makinesiyle Kerberos alanı](#kerberos-join-realm)</span><span class="sxs-lookup"><span data-stu-id="1bb2b-261">Option 1: [Join gateway machine in Kerberos realm](#kerberos-join-realm)</span></span>
* <span data-ttu-id="1bb2b-262">Seçenek 2: [Windows etki alanı Kerberos alanı arasında karşılıklı güven etkinleştir](#kerberos-mutual-trust)</span><span class="sxs-lookup"><span data-stu-id="1bb2b-262">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span></span>

### <span data-ttu-id="1bb2b-263"><a name="kerberos-join-realm"></a>Seçenek 1: ağ geçidi makinesi Kerberos bölgesinde katılın.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-263"><a name="kerberos-join-realm"></a>Option 1: Join gateway machine in Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="1bb2b-264">Gereksinim:</span><span class="sxs-lookup"><span data-stu-id="1bb2b-264">Requirement:</span></span>

* <span data-ttu-id="1bb2b-265">Merhaba ağ geçidi makinesi toojoin hello Kerberos alanı gerektiriyor ve herhangi bir Windows etki alanına katılamıyor.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-265">hello gateway machine needs toojoin hello Kerberos realm and can’t join any Windows domain.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="1bb2b-266">Nasıl tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="1bb2b-266">How tooconfigure:</span></span>

<span data-ttu-id="1bb2b-267">**Ağ geçidi makinede:**</span><span class="sxs-lookup"><span data-stu-id="1bb2b-267">**On gateway machine:**</span></span>

1.  <span data-ttu-id="1bb2b-268">Merhaba çalıştırmak **Ksetup** yardımcı programı tooconfigure hello Kerberos KDC sunucu ve bölge.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-268">Run hello **Ksetup** utility tooconfigure hello Kerberos KDC server and realm.</span></span>

    <span data-ttu-id="1bb2b-269">Kerberos alanı bir Windows etki alanından farklı olduğundan hello makine bir çalışma grubunun bir üyesi yapılandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-269">hello machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span></span> <span data-ttu-id="1bb2b-270">Bu işlem, hello Kerberos alanı ayarlama ve şu şekilde bir KDC sunucusu eklemeyi de yararlanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-270">This can be achieved by setting hello Kerberos realm and adding a KDC server as follows.</span></span> <span data-ttu-id="1bb2b-271">Değiştir *REALM.COM* gerektiği gibi ilgili kendi bölge ile.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-271">Replace *REALM.COM* with your own respective realm as needed.</span></span>

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    <span data-ttu-id="1bb2b-272">**Yeniden** hello makineyi 2 Bu komutları yürütülürken sonra.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-272">**Restart** hello machine after executing these 2 commands.</span></span>

2.  <span data-ttu-id="1bb2b-273">Merhaba yapılandırmayla doğrulayın **Ksetup** komutu.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-273">Verify hello configuration with **Ksetup** command.</span></span> <span data-ttu-id="1bb2b-274">Merhaba çıktısı gibi olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="1bb2b-274">hello output should be like:</span></span>

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

<span data-ttu-id="1bb2b-275">**Azure Data Factory'de:**</span><span class="sxs-lookup"><span data-stu-id="1bb2b-275">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="1bb2b-276">Merhaba HDFS Bağlayıcısı'nı kullanarak yapılandırma **Windows kimlik doğrulaması** Kerberos asıl adı ve parola tooconnect toohello HDFS veri kaynağınız ile birlikte.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-276">Configure hello HDFS connector using **Windows authentication** together with your Kerberos principal name and password tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="1bb2b-277">Denetleme [HDFS bağlantılı hizmet özellikleri](#linked-service-properties) yapılandırma ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-277">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

### <span data-ttu-id="1bb2b-278"><a name="kerberos-mutual-trust"></a>Seçenek 2: Windows etki alanı Kerberos alanı arasında karşılıklı güven etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="1bb2b-278"><a name="kerberos-mutual-trust"></a>Option 2: Enable mutual trust between Windows domain and Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="1bb2b-279">Gereksinim:</span><span class="sxs-lookup"><span data-stu-id="1bb2b-279">Requirement:</span></span>
*   <span data-ttu-id="1bb2b-280">Merhaba ağ geçidi makinesi bir Windows etki alanına katılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-280">hello gateway machine must join a Windows domain.</span></span>
*   <span data-ttu-id="1bb2b-281">İzni tooupdate hello etki alanı denetleyicisinin ayarlarının gerekir.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-281">You need permission tooupdate hello domain controller's settings.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="1bb2b-282">Nasıl tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="1bb2b-282">How tooconfigure:</span></span>

> [!NOTE]
> <span data-ttu-id="1bb2b-283">REALM.COM ve AD.COM gerektiği gibi ilgili kendi bölge ve etki alanı denetleyicisi bu öğreticiyi izleyerek hello değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-283">Replace REALM.COM and AD.COM in hello following tutorial with your own respective realm and domain controller as needed.</span></span>

<span data-ttu-id="1bb2b-284">**KDC sunucusunda:**</span><span class="sxs-lookup"><span data-stu-id="1bb2b-284">**On KDC server:**</span></span>

1.  <span data-ttu-id="1bb2b-285">Merhaba KDC yapılandırmasında Düzenle **krb5.conf** dosya toolet KDC Windows yapılandırma şablonu aşağıdaki toohello başvuran etki alanı güven.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-285">Edit hello KDC configuration in **krb5.conf** file toolet KDC trust Windows Domain referring toohello following configuration template.</span></span> <span data-ttu-id="1bb2b-286">Varsayılan olarak, hello yapılandırması bulunur **/etc/krb5.conf**.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-286">By default, hello configuration is located at **/etc/krb5.conf**.</span></span>

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  <span data-ttu-id="1bb2b-287">**Yeniden** hello KDC Hizmeti yapılandırmasından sonra.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-287">**Restart** hello KDC service after configuration.</span></span>

2.  <span data-ttu-id="1bb2b-288">Adlı bir asıl hazırlama  **krbtgt/REALM.COM@AD.COM**  komutu aşağıdaki hello ile KDC Server'daki:</span><span class="sxs-lookup"><span data-stu-id="1bb2b-288">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with hello following command:</span></span>

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  <span data-ttu-id="1bb2b-289">İçinde **hadoop.security.auth_to_local** HDFS hizmet yapılandırma dosyası, ekleme `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-289">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span></span>

<span data-ttu-id="1bb2b-290">**Etki alanı denetleyicisinde:**</span><span class="sxs-lookup"><span data-stu-id="1bb2b-290">**On domain controller:**</span></span>

1.  <span data-ttu-id="1bb2b-291">Merhaba aşağıdaki komutu çalıştırarak **Ksetup** tooadd bir bölge girişi komutlar:</span><span class="sxs-lookup"><span data-stu-id="1bb2b-291">Run hello following **Ksetup** commands tooadd a realm entry:</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  <span data-ttu-id="1bb2b-292">Windows etki alanı tooKerberos bölge gelen güven oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-292">Establish trust from Windows Domain tooKerberos Realm.</span></span> <span data-ttu-id="1bb2b-293">[paroladır] hello asıl hello parolasını  **krbtgt/REALM.COM@AD.COM** .</span><span class="sxs-lookup"><span data-stu-id="1bb2b-293">[password] is hello password for hello principal **krbtgt/REALM.COM@AD.COM**.</span></span>

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  <span data-ttu-id="1bb2b-294">İçinde Kerberos kullanılan şifreleme algoritmasını seçin.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-294">Select encryption algorithm used in Kerberos.</span></span>

    1. <span data-ttu-id="1bb2b-295">TooServer Yöneticisi Git > Grup İlkesi Yönetimi > etki alanı > Grup İlkesi nesneleri > Varsayılan veya etkin etki alanı ilkesi ve düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-295">Go tooServer Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span></span>

    2. <span data-ttu-id="1bb2b-296">Merhaba, **Grup İlkesi Yönetimi Düzenleyicisi** açılan pencerede, Git tooComputer yapılandırma > ilkeler > Windows Ayarları > Güvenlik Ayarları > yerel ilkeler > güvenlik seçenekleri ve yapılandırma **ağ Güvenlik: Kerberos için izin verilen şifreleme türleri yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-296">In hello **Group Policy Management Editor** popup window, go tooComputer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span></span>

    3. <span data-ttu-id="1bb2b-297">Select hello şifreleme algoritması toouse istediğiniz tooKDC bağladığınızda.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-297">Select hello encryption algorithm you want toouse when connect tooKDC.</span></span> <span data-ttu-id="1bb2b-298">Genellikle, yalnızca tüm hello seçeneklerini belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-298">Commonly, you can simply select all hello options.</span></span>

        ![Kerberos için yapılandırma şifreleme türleri](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. <span data-ttu-id="1bb2b-300">Kullanım **Ksetup** komutu toospecify hello şifreleme algoritması toobe hello üzerinde kullanılan belirli bölgesi.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-300">Use **Ksetup** command toospecify hello encryption algorithm toobe used on hello specific REALM.</span></span>

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  <span data-ttu-id="1bb2b-301">Merhaba etki alanı hesabını ve Kerberos arasında Hello eşleme sipariş toouse Windows etki alanında Kerberos asıl asıl oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-301">Create hello mapping between hello domain account and Kerberos principal, in order toouse Kerberos principal in Windows Domain.</span></span>

    1. <span data-ttu-id="1bb2b-302">Merhaba yönetimsel araçları başlatmak > **Active Directory Kullanıcıları ve Bilgisayarları**.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-302">Start hello Administrative tools > **Active Directory Users and Computers**.</span></span>

    2. <span data-ttu-id="1bb2b-303">Tıklayarak Gelişmiş özellikleri yapılandırma **Görünüm** > **Gelişmiş Özellikler**.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-303">Configure advanced features by clicking **View** > **Advanced Features**.</span></span>

    3. <span data-ttu-id="1bb2b-304">Toocreate eşlemeleri istediğiniz ve tooview sağ hello hesap toowhich bulun **adı eşlemeleri** > tıklatın **Kerberos adları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-304">Locate hello account toowhich you want toocreate mappings, and right-click tooview **Name Mappings** > click **Kerberos Names** tab.</span></span>

    4. <span data-ttu-id="1bb2b-305">Sorumlu hello Bölgesi ' ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-305">Add a principal from hello realm.</span></span>

        ![Güvenlik kimliğine eşleyin](media/data-factory-hdfs-connector/map-security-identity.png)

<span data-ttu-id="1bb2b-307">**Ağ geçidi makinede:**</span><span class="sxs-lookup"><span data-stu-id="1bb2b-307">**On gateway machine:**</span></span>

* <span data-ttu-id="1bb2b-308">Merhaba aşağıdaki komutu çalıştırarak **Ksetup** tooadd bir bölge girişi komutları.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-308">Run hello following **Ksetup** commands tooadd a realm entry.</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

<span data-ttu-id="1bb2b-309">**Azure Data Factory'de:**</span><span class="sxs-lookup"><span data-stu-id="1bb2b-309">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="1bb2b-310">Merhaba HDFS Bağlayıcısı'nı kullanarak yapılandırma **Windows kimlik doğrulaması** etki alanı hesabı veya Kerberos asıl tooconnect toohello HDFS veri kaynağı ile birlikte.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-310">Configure hello HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="1bb2b-311">Denetleme [HDFS bağlantılı hizmet özellikleri](#linked-service-properties) yapılandırma ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-311">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

> [!NOTE]
> <span data-ttu-id="1bb2b-312">Kaynak veri kümesi toocolumns havuz kümesinden toomap sütunlarından bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="1bb2b-312">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="performance-and-tuning"></a><span data-ttu-id="1bb2b-313">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="1bb2b-313">Performance and Tuning</span></span>
<span data-ttu-id="1bb2b-314">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-314">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
