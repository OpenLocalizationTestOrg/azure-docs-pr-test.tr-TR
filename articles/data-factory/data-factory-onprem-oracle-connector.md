---
title: / Data Factory kullanarak Oracle aaaCopy verileri | Microsoft Docs
description: "Nasıl toocopy veri için/olan Oracle veritabanından Azure Data Factory kullanarak şirket içi öğrenin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="e286d-103">Öğesine/öğesinden Azure Data Factory kullanarak şirket içi Oracle veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="e286d-103">Copy data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="e286d-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove veri grafikten bir şirket içi Oracle veritabanına açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e286d-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="e286d-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="e286d-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="e286d-106">Desteklenen senaryolar</span><span class="sxs-lookup"><span data-stu-id="e286d-106">Supported scenarios</span></span>
<span data-ttu-id="e286d-107">Veri kopyalama **bir Oracle veritabanından** veri depolarına aşağıdaki toohello:</span><span class="sxs-lookup"><span data-stu-id="e286d-107">You can copy data **from an Oracle database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="e286d-108">Veri depoları aşağıdaki hello verileri kopyalayabilirsiniz **tooan Oracle veritabanı**:</span><span class="sxs-lookup"><span data-stu-id="e286d-108">You can copy data from hello following data stores **tooan Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="e286d-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e286d-109">Prerequisites</span></span>
<span data-ttu-id="e286d-110">Veri Fabrikası hello veri yönetimi ağ geçidi kullanarak bağlanan tooon içi Oracle kaynakları destekler.</span><span class="sxs-lookup"><span data-stu-id="e286d-110">Data Factory supports connecting tooon-premises Oracle sources using hello Data Management Gateway.</span></span> <span data-ttu-id="e286d-111">Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) makale toolearn veri yönetimi ağ geçidi hakkında ve [şirket içi toocloud veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale hello ağ geçidi kurun veri ardışık ayarlama hakkında adım adım yönergeler için toomove verileri.</span><span class="sxs-lookup"><span data-stu-id="e286d-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article toolearn about Data Management Gateway and [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="e286d-112">Merhaba Oracle bir Azure Iaas sanal barındırılan olsa bile ağ geçidi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e286d-112">Gateway is required even if hello Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="e286d-113">Merhaba ağ geçidi üzerinde aynı Iaas VM hello veri olarak depolamak veya hello ağ geçidi olarak aynı uzunlukta farklı bir VM üzerinde toohello veritabanı bağlanabilir hello yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e286d-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="e286d-114">Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="e286d-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="e286d-115">Desteklenen sürümleri ve yükleme</span><span class="sxs-lookup"><span data-stu-id="e286d-115">Supported versions and installation</span></span>
<span data-ttu-id="e286d-116">Bu Oracle bağlayıcı sürücülerin iki sürümlerini destekler:</span><span class="sxs-lookup"><span data-stu-id="e286d-116">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="e286d-117">**(Önerilen) Oracle için Microsoft sürücüsü**: Oracle hello ağ geçidi ile birlikte otomatik olarak yüklenen için veri yönetimi ağ geçidi'nden sürüm 2.7, Microsoft sürücüsü başlayarak, bu nedenle yapmanıza gerek yoktur sırayla tooadditionally tanıtıcı hello sürücüsü Ayrıca tooestablish bağlantı tooOracle ve bu sürücü kullanarak daha iyi kopyalama performansını yaşayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e286d-117">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with hello gateway, so you don't need tooadditionally handle hello driver in order tooestablish connectivity tooOracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="e286d-118">Oracle sürümleri veritabanları desteklenir:</span><span class="sxs-lookup"><span data-stu-id="e286d-118">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="e286d-119">Oracle 12c R1 (12,1)</span><span class="sxs-lookup"><span data-stu-id="e286d-119">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="e286d-120">Oracle 11g R1, R2 (11.1, 11.2)</span><span class="sxs-lookup"><span data-stu-id="e286d-120">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="e286d-121">Oracle 10g R1, R2 (10,1, 10.2)</span><span class="sxs-lookup"><span data-stu-id="e286d-121">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="e286d-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span><span class="sxs-lookup"><span data-stu-id="e286d-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="e286d-123">Oracle 8i R3 (8.1.7)</span><span class="sxs-lookup"><span data-stu-id="e286d-123">Oracle 8i R3 (8.1.7)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e286d-124">Şu anda Oracle için Microsoft sürücüsü yalnızca Oracle ancak tooOracle yazılamıyor veri kopyalamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="e286d-124">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing tooOracle.</span></span> <span data-ttu-id="e286d-125">Ve Not hello test bağlantısı özelliği veri yönetimi ağ geçidi tanılama sekmesinde bu sürücüyü desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="e286d-125">And note hello test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="e286d-126">Alternatif olarak, hello Kopyalama Sihirbazı'nı toovalidate hello bağlantısını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e286d-126">Alternatively, you can use hello copy wizard toovalidate hello connectivity.</span></span>
>

- <span data-ttu-id="e286d-127">**.NET için Oracle veri sağlayıcısı:** toouse Oracle veri sağlayıcısı toocopy verileri de seçebilirsiniz / tooOracle.</span><span class="sxs-lookup"><span data-stu-id="e286d-127">**Oracle Data Provider for .NET:** you can also choose toouse Oracle Data Provider toocopy data from/tooOracle.</span></span> <span data-ttu-id="e286d-128">Bu bileşen dahil [için Oracle veri erişim bileşenleri Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e286d-128">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="e286d-129">Merhaba uygun sürüm (32/64 bit) hello ağ geçidi yüklendiği hello makineye yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e286d-129">Install hello appropriate version (32/64 bit) on hello machine where hello gateway is installed.</span></span> <span data-ttu-id="e286d-130">[Oracle veri sağlayıcısı .NET 12,1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) tooOracle veritabanı 10 g sürüm 2 veya sonrasını erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e286d-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access tooOracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="e286d-131">"XCopy yükleme" seçerseniz, hello readme.htm adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e286d-131">If you choose “XCopy Installation”, follow steps in hello readme.htm.</span></span> <span data-ttu-id="e286d-132">Kullanıcı Arabirimi (olmayan-XCopy biri) ile Merhaba yükleyici seçtiğiniz öneririz.</span><span class="sxs-lookup"><span data-stu-id="e286d-132">We recommend you choose hello installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="e286d-133">Merhaba sağlayıcı yükledikten sonra **yeniden** hello Hizmetleri uygulaması (veya) veri yönetimi ağ geçidi Yapılandırma Yöneticisi kullanarak makinenizde veri yönetimi ağ geçidi ana bilgisayar hizmeti.</span><span class="sxs-lookup"><span data-stu-id="e286d-133">After installing hello provider, **restart** hello Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="e286d-134">Kopyalama Sihirbazı'nı tooauthor hello kopyalama işlem hattını kullanırsanız, otomatik olarak belirlenen hello sürücü türü olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e286d-134">If you use copy wizard tooauthor hello copy pipeline, hello driver type will be auto-determined.</span></span> <span data-ttu-id="e286d-135">Microsoft sürücüsü, ağ geçidi sürümü 2.7 düşük olduğu veya Oracle havuz olarak seçtiğiniz sürece varsayılan olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e286d-135">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="e286d-136">Başlarken</span><span class="sxs-lookup"><span data-stu-id="e286d-136">Getting started</span></span>
<span data-ttu-id="e286d-137">Farklı araçlar/API'lerini kullanarak bir şirket içi Oracle veritabanından/gelen verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e286d-137">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="e286d-138">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="e286d-138">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="e286d-139">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="e286d-139">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="e286d-140">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="e286d-140">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="e286d-141">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="e286d-141">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="e286d-142">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="e286d-142">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="e286d-143">Oluşturma bir **veri fabrikası**.</span><span class="sxs-lookup"><span data-stu-id="e286d-143">Create a **data factory**.</span></span> <span data-ttu-id="e286d-144">Veri Fabrikası bir veya daha fazla ardışık düzen içerebilir.</span><span class="sxs-lookup"><span data-stu-id="e286d-144">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="e286d-145">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="e286d-145">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="e286d-146">Bir Oralce veritabanı tooan Azure blob depolama veri kopyalama, örneğin, iki bağlı hizmet toolink Oracle veritabanı ve Azure depolama hesabı tooyour veri fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e286d-146">For example, if you are copying data from an Oralce database tooan Azure blob storage, you create two linked services toolink your Oracle database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="e286d-147">Belirli tooOracle bağlantılı hizmet özellikler için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="e286d-147">For linked service properties that are specific tooOracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="e286d-148">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="e286d-148">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="e286d-149">Merhaba son adımda bahsedilen hello örnekte, Oracle veritabanınız hello giriş verileri içeren bir veri kümesi toospecify hello tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e286d-149">In hello example mentioned in hello last step, you create a dataset toospecify hello table in your Oracle database that contains hello input data.</span></span> <span data-ttu-id="e286d-150">Başka bir veri kümesi toospecify hello blob kapsayıcı oluşturun ve hello verilerini tutan hello klasörü hello Oracle veritabanı kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="e286d-150">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello Oracle database.</span></span> <span data-ttu-id="e286d-151">Belirli tooOracle dataset özellikler için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="e286d-151">For dataset properties that are specific tooOracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="e286d-152">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="e286d-152">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="e286d-153">Daha önce bahsedilen hello örnekte OracleSource bir kaynak ve BlobSink havuzu olarak hello kopya etkinliği için kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="e286d-153">In hello example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="e286d-154">Azure Blob Storage tooOracle veritabanı ' kopyalıyorsanız benzer şekilde, BlobSource ve OracleSink hello kopyalama etkinliği kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="e286d-154">Similarly, if you are copying from Azure Blob Storage tooOracle Database, you use BlobSource and OracleSink in hello copy activity.</span></span> <span data-ttu-id="e286d-155">Belirli tooOracle veritabanı kopyalama etkinliği özellikler için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="e286d-155">For copy activity properties that are specific tooOracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="e286d-156">Nasıl toouse bir veri deposu bir kaynak veya bir havuz olarak hakkında daha fazla bilgi için veri deposu hello önceki bölümdeki hello bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e286d-156">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="e286d-157">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e286d-157">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="e286d-158">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="e286d-158">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="e286d-159">Şirket içi Oracle veritabanına/kullanılan toocopy verileri olan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples-for-copying-data-to-and-from-oracle-database) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="e286d-159">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="e286d-160">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıklarını olan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="e286d-160">hello following sections provide details about JSON properties that are used toodefine Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="e286d-161">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="e286d-161">Linked service properties</span></span>
<span data-ttu-id="e286d-162">Aşağıdaki tablonun hello JSON öğeleri belirli tooOracle bağlantılı hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="e286d-162">hello following table provides description for JSON elements specific tooOracle linked service.</span></span>

| <span data-ttu-id="e286d-163">Özellik</span><span class="sxs-lookup"><span data-stu-id="e286d-163">Property</span></span> | <span data-ttu-id="e286d-164">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e286d-164">Description</span></span> | <span data-ttu-id="e286d-165">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e286d-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e286d-166">type</span><span class="sxs-lookup"><span data-stu-id="e286d-166">type</span></span> |<span data-ttu-id="e286d-167">Merhaba type özelliği ayarlanmalıdır: **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="e286d-167">hello type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="e286d-168">Evet</span><span class="sxs-lookup"><span data-stu-id="e286d-168">Yes</span></span> |
| <span data-ttu-id="e286d-169">driverType</span><span class="sxs-lookup"><span data-stu-id="e286d-169">driverType</span></span> | <span data-ttu-id="e286d-170">Hangi sürücü toouse toocopy verilerden belirtin / tooOracle veritabanı.</span><span class="sxs-lookup"><span data-stu-id="e286d-170">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="e286d-171">İzin verilen değerler **Microsoft** veya **ODP** (varsayılan).</span><span class="sxs-lookup"><span data-stu-id="e286d-171">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="e286d-172">Bkz: [desteklenen sürümü ve yükleme](#supported-versions-and-installation) sürücü ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="e286d-172">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="e286d-173">Hayır</span><span class="sxs-lookup"><span data-stu-id="e286d-173">No</span></span> |
| <span data-ttu-id="e286d-174">connectionString</span><span class="sxs-lookup"><span data-stu-id="e286d-174">connectionString</span></span> | <span data-ttu-id="e286d-175">Tooconnect toohello Oracle veritabanı örneği hello connectionString özelliği için gerekli bilgiler belirtin.</span><span class="sxs-lookup"><span data-stu-id="e286d-175">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="e286d-176">Evet</span><span class="sxs-lookup"><span data-stu-id="e286d-176">Yes</span></span> |
| <span data-ttu-id="e286d-177">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e286d-177">gatewayName</span></span> | <span data-ttu-id="e286d-178">Kullanılan tooconnect toohello olan şirket içi Oracle Sunucusu hello ağ geçidi adı</span><span class="sxs-lookup"><span data-stu-id="e286d-178">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="e286d-179">Evet</span><span class="sxs-lookup"><span data-stu-id="e286d-179">Yes</span></span> |

<span data-ttu-id="e286d-180">**Örnek: Microsoft sürücüsü kullanma:**</span><span class="sxs-lookup"><span data-stu-id="e286d-180">**Example: using Microsoft driver:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="e286d-181">**Örnek: ODP sürücü kullanma**</span><span class="sxs-lookup"><span data-stu-id="e286d-181">**Example: using ODP driver**</span></span>

<span data-ttu-id="e286d-182">Çok başvuran[bu site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) biçimleri hello için.</span><span class="sxs-lookup"><span data-stu-id="e286d-182">Refer too[this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for hello allowed formats.</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="e286d-183">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="e286d-183">Dataset properties</span></span>
<span data-ttu-id="e286d-184">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="e286d-184">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="e286d-185">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Oracle, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="e286d-185">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="e286d-186">Merhaba typeProperties bölümü veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e286d-186">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="e286d-187">türü OracleTable hello veri kümesi için Hello typeProperties bölümü hello aşağıdaki özelliklere sahip:</span><span class="sxs-lookup"><span data-stu-id="e286d-187">hello typeProperties section for hello dataset of type OracleTable has hello following properties:</span></span>

| <span data-ttu-id="e286d-188">Özellik</span><span class="sxs-lookup"><span data-stu-id="e286d-188">Property</span></span> | <span data-ttu-id="e286d-189">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e286d-189">Description</span></span> | <span data-ttu-id="e286d-190">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e286d-190">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e286d-191">tableName</span><span class="sxs-lookup"><span data-stu-id="e286d-191">tableName</span></span> |<span data-ttu-id="e286d-192">Merhaba bağlantılı hizmet hello Oracle veritabanı Merhaba tablonun adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e286d-192">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="e286d-193">Hayır (varsa **oracleReaderQuery** , **OracleSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="e286d-193">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="e286d-194">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="e286d-194">Copy activity properties</span></span>
<span data-ttu-id="e286d-195">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="e286d-195">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="e286d-196">Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e286d-196">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="e286d-197">Merhaba kopyalama etkinliği yalnızca bir girdi alır ve tek bir çıktı üretir.</span><span class="sxs-lookup"><span data-stu-id="e286d-197">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="e286d-198">Oysa hello typeProperties bölümünde hello etkinlik özellikleri her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="e286d-198">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="e286d-199">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="e286d-199">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="e286d-200">OracleSource</span><span class="sxs-lookup"><span data-stu-id="e286d-200">OracleSource</span></span>
<span data-ttu-id="e286d-201">Kopyalama etkinliğinde hello kaynak türü olduğunda **OracleSource** aşağıdaki özelliklere hello kullanılabilir **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="e286d-201">In Copy activity, when hello source is of type **OracleSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="e286d-202">Özellik</span><span class="sxs-lookup"><span data-stu-id="e286d-202">Property</span></span> | <span data-ttu-id="e286d-203">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e286d-203">Description</span></span> | <span data-ttu-id="e286d-204">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="e286d-204">Allowed values</span></span> | <span data-ttu-id="e286d-205">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e286d-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e286d-206">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="e286d-206">oracleReaderQuery</span></span> |<span data-ttu-id="e286d-207">Merhaba özel sorgu tooread verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="e286d-207">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e286d-208">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="e286d-208">SQL query string.</span></span> <span data-ttu-id="e286d-209">Örneğin: seçin * from MyTable</span><span class="sxs-lookup"><span data-stu-id="e286d-209">For example: select * from MyTable</span></span> <br/><br/><span data-ttu-id="e286d-210">Belirtilmezse, yürütülen SQL deyimini hello: seçin * from MyTable</span><span class="sxs-lookup"><span data-stu-id="e286d-210">If not specified, hello SQL statement that is executed: select * from MyTable</span></span> |<span data-ttu-id="e286d-211">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="e286d-211">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="e286d-212">OracleSink</span><span class="sxs-lookup"><span data-stu-id="e286d-212">OracleSink</span></span>
<span data-ttu-id="e286d-213">**OracleSink** aşağıdaki özelliklere hello destekler:</span><span class="sxs-lookup"><span data-stu-id="e286d-213">**OracleSink** supports hello following properties:</span></span>

| <span data-ttu-id="e286d-214">Özellik</span><span class="sxs-lookup"><span data-stu-id="e286d-214">Property</span></span> | <span data-ttu-id="e286d-215">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e286d-215">Description</span></span> | <span data-ttu-id="e286d-216">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="e286d-216">Allowed values</span></span> | <span data-ttu-id="e286d-217">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e286d-217">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e286d-218">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="e286d-218">writeBatchTimeout</span></span> |<span data-ttu-id="e286d-219">Zaman aşımına uğramadan önce hello toplu ekleme işlemi toocomplete bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="e286d-219">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="e286d-220">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e286d-220">timespan</span></span><br/><br/> <span data-ttu-id="e286d-221">Örnek: 00:30:00 (30 dakika).</span><span class="sxs-lookup"><span data-stu-id="e286d-221">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="e286d-222">Hayır</span><span class="sxs-lookup"><span data-stu-id="e286d-222">No</span></span> |
| <span data-ttu-id="e286d-223">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="e286d-223">writeBatchSize</span></span> |<span data-ttu-id="e286d-224">Merhaba arabellek boyutu writeBatchSize ulaştığında veri hello SQL tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="e286d-224">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="e286d-225">Tamsayı (satır sayısı)</span><span class="sxs-lookup"><span data-stu-id="e286d-225">Integer (number of rows)</span></span> |<span data-ttu-id="e286d-226">Hayır (varsayılan: 100)</span><span class="sxs-lookup"><span data-stu-id="e286d-226">No (default: 100)</span></span> |
| <span data-ttu-id="e286d-227">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="e286d-227">sqlWriterCleanupScript</span></span> |<span data-ttu-id="e286d-228">Belirli bir dilimle verilerinin temizlenmesini gibi bir sorgu için kopyalama etkinliği tooexecute belirtin.</span><span class="sxs-lookup"><span data-stu-id="e286d-228">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="e286d-229">Sorgu bildirimi.</span><span class="sxs-lookup"><span data-stu-id="e286d-229">A query statement.</span></span> |<span data-ttu-id="e286d-230">Hayır</span><span class="sxs-lookup"><span data-stu-id="e286d-230">No</span></span> |
| <span data-ttu-id="e286d-231">Sliceıdentifiercolumnname</span><span class="sxs-lookup"><span data-stu-id="e286d-231">sliceIdentifierColumnName</span></span> |<span data-ttu-id="e286d-232">Kopyalama etkinliği toofill sütun adı, ne zaman yeniden çalıştırılacağını belirli bir dilim verilerini kullanılan tooclean olduğu otomatik dilim tanımlayıcı ile belirtin.</span><span class="sxs-lookup"><span data-stu-id="e286d-232">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="e286d-233">Binary(32) veri türüne sahip bir sütunun sütun adı.</span><span class="sxs-lookup"><span data-stu-id="e286d-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="e286d-234">Hayır</span><span class="sxs-lookup"><span data-stu-id="e286d-234">No</span></span> |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a><span data-ttu-id="e286d-235">Oracle veritabanından veri tooand kopyalamak için JSON örnekleri</span><span class="sxs-lookup"><span data-stu-id="e286d-235">JSON examples for copying data tooand from Oracle database</span></span>
<span data-ttu-id="e286d-236">Merhaba aşağıdaki örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e286d-236">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="e286d-237">Bunlar Göster nasıl toocopy verilerden / tooan Oracle veritabanı/Azure Blob depolama biriminden.</span><span class="sxs-lookup"><span data-stu-id="e286d-237">They show how toocopy data from/tooan Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="e286d-238">Ancak, veri belirtildiği hello havuzlarını, kopyalanan tooany olabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="e286d-238">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a><span data-ttu-id="e286d-239">Örnek: Verilerini Oracle tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="e286d-239">Example: Copy data from Oracle tooAzure Blob</span></span>

<span data-ttu-id="e286d-240">Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="e286d-240">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="e286d-241">Bağlı hizmet türü [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e286d-241">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="e286d-242">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e286d-242">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="e286d-243">Bir giriş [dataset](data-factory-create-datasets.md) türü [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e286d-243">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="e286d-244">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e286d-244">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="e286d-245">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) kaynağı olarak ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) havuz olarak.</span><span class="sxs-lookup"><span data-stu-id="e286d-245">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="e286d-246">Merhaba örnek verileri bir tabloda bir şirket içi Oracle veritabanı tooa blob saatlik kopyalar.</span><span class="sxs-lookup"><span data-stu-id="e286d-246">hello sample copies data from a table in an on-premises Oracle database tooa blob hourly.</span></span> <span data-ttu-id="e286d-247">Merhaba örnekte kullanılan çeşitli özellikler hakkında daha fazla bilgi için hello örnekleri aşağıdaki bölümlerde belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="e286d-247">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="e286d-248">**Oracle bağlantılı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="e286d-248">**Oracle linked service:**</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="e286d-249">**Azure Blob storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="e286d-249">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="e286d-250">**Oracle girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="e286d-250">**Oracle input dataset:**</span></span>

<span data-ttu-id="e286d-251">Merhaba örnek Oracle tablo "MyTable" oluşturulur ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="e286d-251">hello sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="e286d-252">"Dış" ayarı: "true" bildirir hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="e286d-252">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
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

<span data-ttu-id="e286d-253">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="e286d-253">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="e286d-254">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="e286d-254">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e286d-255">Merhaba klasör yolu ve dosya adını hello blob dinamik olarak değerlendirilir işleniyor hello dilimin hello başlangıç zamanı temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="e286d-255">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="e286d-256">Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="e286d-256">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
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

<span data-ttu-id="e286d-257">**Kopyalama etkinliği ile kanal:**</span><span class="sxs-lookup"><span data-stu-id="e286d-257">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="e286d-258">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun saatlik ise.</span><span class="sxs-lookup"><span data-stu-id="e286d-258">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="e286d-259">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**OracleSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="e286d-259">In hello pipeline JSON definition, hello **source** type is set too**OracleSource** and **sink** type is set too**BlobSink**.</span></span>  <span data-ttu-id="e286d-260">Merhaba SQL sorgusu ile belirtilen **oracleReaderQuery** özelliği saat toocopy geçmiş hello hello veri seçer.</span><span class="sxs-lookup"><span data-stu-id="e286d-260">hello SQL query specified with **oracleReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

## <a name="example-copy-data-from-azure-blob-toooracle"></a><span data-ttu-id="e286d-261">Örnek: Verilerini Azure Blob tooOracle</span><span class="sxs-lookup"><span data-stu-id="e286d-261">Example: Copy data from Azure Blob tooOracle</span></span>
<span data-ttu-id="e286d-262">Bu örnek nasıl toocopy verileri Azure Blob Storage tooan Oracle veritabanı şirket içi gösterir.</span><span class="sxs-lookup"><span data-stu-id="e286d-262">This sample shows how toocopy data from an Azure Blob Storage tooan on-premises Oracle database.</span></span> <span data-ttu-id="e286d-263">Ancak, veriler kopyalanabilir **doğrudan** herhangi belirtildiği hello kaynakları [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="e286d-263">However, data can be copied **directly** from any of hello sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="e286d-264">Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="e286d-264">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="e286d-265">Bağlı hizmet türü [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e286d-265">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="e286d-266">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e286d-266">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="e286d-267">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e286d-267">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="e286d-268">Bir çıkış [dataset](data-factory-create-datasets.md) türü [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e286d-268">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="e286d-269">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) kaynağı olarak [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) havuz olarak.</span><span class="sxs-lookup"><span data-stu-id="e286d-269">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="e286d-270">Merhaba örnek verileri saatte bir şirket içi Oracle veritabanına bir blob tooa tablodaki kopyalar.</span><span class="sxs-lookup"><span data-stu-id="e286d-270">hello sample copies data from a blob tooa table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="e286d-271">Merhaba örnekte kullanılan çeşitli özellikler hakkında daha fazla bilgi için hello örnekleri aşağıdaki bölümlerde belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="e286d-271">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="e286d-272">**Oracle bağlantılı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="e286d-272">**Oracle linked service:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="e286d-273">**Azure Blob storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="e286d-273">**Azure Blob storage linked service:**</span></span>
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="e286d-274">**Azure Blob girdi veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="e286d-274">**Azure Blob input dataset**</span></span>

<span data-ttu-id="e286d-275">Veri toplanma yeni blob üzerinden saatte (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="e286d-275">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e286d-276">Merhaba klasör yolu ve dosya adını hello blob dinamik olarak değerlendirilir işleniyor hello dilimin hello başlangıç zamanı temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="e286d-276">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="e286d-277">Merhaba klasör yolu yıl, ay ve gün kısmını hello başlangıç saati ve dosya adı hello başlangıç saati hello saat bölümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="e286d-277">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="e286d-278">"dış": "true" ayarı bu tablosu dış toohello veri fabrikası ve hello veri fabrikasında bir etkinlik tarafından üretilen değil hello Data Factory hizmetinin sizi bilgilendirir.</span><span class="sxs-lookup"><span data-stu-id="e286d-278">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
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
                }
            ],
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Day",
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

<span data-ttu-id="e286d-279">**Oracle çıktı veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="e286d-279">**Oracle output dataset:**</span></span>

<span data-ttu-id="e286d-280">Hello örnek Oracle tablo "MyTable" oluşturdunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="e286d-280">hello sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="e286d-281">Oracle ile Merhaba tablosunu oluşturan hello Blob CSV dosyası toocontain beklediğiniz gibi hello aynı sayıda sütun.</span><span class="sxs-lookup"><span data-stu-id="e286d-281">Create hello table in Oracle with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="e286d-282">Yeni satırlar toohello tablo saatte eklenir.</span><span class="sxs-lookup"><span data-stu-id="e286d-282">New rows are added toohello table every hour.</span></span>

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

<span data-ttu-id="e286d-283">**Kopyalama etkinliği ile kanal:**</span><span class="sxs-lookup"><span data-stu-id="e286d-283">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="e286d-284">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="e286d-284">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="e286d-285">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**BlobSource** ve hello **havuz** türü olarak ayarlanmış çok**OracleSink**.</span><span class="sxs-lookup"><span data-stu-id="e286d-285">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and hello **sink** type is set too**OracleSink**.</span></span>  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
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


## <a name="troubleshooting-tips"></a><span data-ttu-id="e286d-286">Sorun giderme ipuçları</span><span class="sxs-lookup"><span data-stu-id="e286d-286">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="e286d-287">Sorun 1: .NET Framework veri sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="e286d-287">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="e286d-288">Merhaba aşağıdakilere bakın **hata iletisi**:</span><span class="sxs-lookup"><span data-stu-id="e286d-288">You see hello following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="e286d-289">**Olası nedenler:**</span><span class="sxs-lookup"><span data-stu-id="e286d-289">**Possible causes:**</span></span>

1. <span data-ttu-id="e286d-290">Merhaba Oracle için .NET Framework veri sağlayıcısı yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="e286d-290">hello .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="e286d-291">Merhaba Oracle için .NET Framework veri sağlayıcısı yüklü too.NET Framework 2.0 ve .NET Framework 4.0 hello klasörlerde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="e286d-291">hello .NET Framework Data Provider for Oracle was installed too.NET Framework 2.0 and is not found in hello .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="e286d-292">**Çözümleme/geçici çözüm:**</span><span class="sxs-lookup"><span data-stu-id="e286d-292">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="e286d-293">Merhaba, Oracle için .NET sağlayıcısı yüklemediyseniz [yüklemek](http://www.oracle.com/technetwork/topics/dotnet/downloads/) ve hello senaryo yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="e286d-293">If you haven't installed hello .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry hello scenario.</span></span>
2. <span data-ttu-id="e286d-294">Merhaba sağlayıcı yükledikten sonra bile hello hata iletisi alırsanız, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="e286d-294">If you get hello error message even after installing hello provider, do hello following steps:</span></span>
   1. <span data-ttu-id="e286d-295">Makine yapılandırma .NET 2.0 hello klasöründen açın: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span><span class="sxs-lookup"><span data-stu-id="e286d-295">Open machine config of .NET 2.0 from hello folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="e286d-296">Arama **.NET için Oracle veri sağlayıcısı**, ve hello örnek altında aşağıdaki gösterildiği gibi mümkün toofind bir giriş olmalıdır **system.data** -> **DbProviderFactories**: "<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description=".NET için oracle veri sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="e286d-296">Search for **Oracle Data Provider for .NET**, and you should be able toofind an entry as shown in hello following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="e286d-297">”</span><span class="sxs-lookup"><span data-stu-id="e286d-297">”</span></span>
3. <span data-ttu-id="e286d-298">Bu giriş toohello machine.config dosyasının v4.0 klasörü aşağıdaki hello kopyalayın: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config ve değişiklik hello sürüm too4.xxx.x.x.</span><span class="sxs-lookup"><span data-stu-id="e286d-298">Copy this entry toohello machine.config file in hello following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change hello version too4.xxx.x.x.</span></span>
4. <span data-ttu-id="e286d-299">"< ODP.NET yüklü yolu > \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll" Merhaba Genel Derleme Önbelleği'ne (GAC) çalıştırarak yükleyin `gacutil /i [provider path]`. ## sorun giderme ipuçları</span><span class="sxs-lookup"><span data-stu-id="e286d-299">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into hello global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="e286d-300">Sorun 2: datetime biçimlendirme</span><span class="sxs-lookup"><span data-stu-id="e286d-300">Problem 2: datetime formatting</span></span>

<span data-ttu-id="e286d-301">Merhaba aşağıdakilere bakın **hata iletisi**:</span><span class="sxs-lookup"><span data-stu-id="e286d-301">You see hello following **error message**:</span></span>

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="e286d-302">**Çözümleme/geçici çözüm:**</span><span class="sxs-lookup"><span data-stu-id="e286d-302">**Resolution/Workaround:**</span></span>

<span data-ttu-id="e286d-303">Merhaba aşağıda gösterildiği gibi tarihleri, Oracle veritabanınızı nasıl yapılandırıldığına göre kopyalama etkinliğinde tooadjust hello sorgu dizesi gerekebilir (Merhaba to_date işlevi kullanılarak) örnek:</span><span class="sxs-lookup"><span data-stu-id="e286d-303">You may need tooadjust hello query string in your copy activity based on how dates are configured in your Oracle database, as shown in hello following sample (using hello to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="e286d-304">Oracle için tür eşlemesi</span><span class="sxs-lookup"><span data-stu-id="e286d-304">Type mapping for Oracle</span></span>
<span data-ttu-id="e286d-305">Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale kopyalama etkinliği ile 2 adımlı yaklaşımı izleyerek hello kaynak türleri toosink türlerinden otomatik tür dönüşümleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="e286d-305">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="e286d-306">Yerel kaynak türleri too.NET türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="e286d-306">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="e286d-307">.NET türü toonative havuz türünden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="e286d-307">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="e286d-308">Verileri Oracle'dan taşırken, eşlemeleri aşağıdaki hello Oracle veri türü too.NET türünden ve kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e286d-308">When moving data from Oracle, hello following mappings are used from Oracle data type too.NET type and vice versa.</span></span>

| <span data-ttu-id="e286d-309">Oracle veri türü</span><span class="sxs-lookup"><span data-stu-id="e286d-309">Oracle data type</span></span> | <span data-ttu-id="e286d-310">.NET framework veri türü</span><span class="sxs-lookup"><span data-stu-id="e286d-310">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="e286d-311">BDOSYA</span><span class="sxs-lookup"><span data-stu-id="e286d-311">BFILE</span></span> |<span data-ttu-id="e286d-312">Byte]</span><span class="sxs-lookup"><span data-stu-id="e286d-312">Byte[]</span></span> |
| <span data-ttu-id="e286d-313">BLOB</span><span class="sxs-lookup"><span data-stu-id="e286d-313">BLOB</span></span> |<span data-ttu-id="e286d-314">Byte]</span><span class="sxs-lookup"><span data-stu-id="e286d-314">Byte[]</span></span> |
| <span data-ttu-id="e286d-315">CHAR</span><span class="sxs-lookup"><span data-stu-id="e286d-315">CHAR</span></span> |<span data-ttu-id="e286d-316">Dize</span><span class="sxs-lookup"><span data-stu-id="e286d-316">String</span></span> |
| <span data-ttu-id="e286d-317">CLOB</span><span class="sxs-lookup"><span data-stu-id="e286d-317">CLOB</span></span> |<span data-ttu-id="e286d-318">Dize</span><span class="sxs-lookup"><span data-stu-id="e286d-318">String</span></span> |
| <span data-ttu-id="e286d-319">TARİH</span><span class="sxs-lookup"><span data-stu-id="e286d-319">DATE</span></span> |<span data-ttu-id="e286d-320">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="e286d-320">DateTime</span></span> |
| <span data-ttu-id="e286d-321">KAYAN NOKTA</span><span class="sxs-lookup"><span data-stu-id="e286d-321">FLOAT</span></span> |<span data-ttu-id="e286d-322">Ondalık, dize (varsa precision > 28)</span><span class="sxs-lookup"><span data-stu-id="e286d-322">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="e286d-323">TAMSAYI</span><span class="sxs-lookup"><span data-stu-id="e286d-323">INTEGER</span></span> |<span data-ttu-id="e286d-324">Ondalık, dize (varsa precision > 28)</span><span class="sxs-lookup"><span data-stu-id="e286d-324">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="e286d-325">ARALIĞI yıl tooMONTH</span><span class="sxs-lookup"><span data-stu-id="e286d-325">INTERVAL YEAR tooMONTH</span></span> |<span data-ttu-id="e286d-326">Int32</span><span class="sxs-lookup"><span data-stu-id="e286d-326">Int32</span></span> |
| <span data-ttu-id="e286d-327">Aralık gün tooSECOND</span><span class="sxs-lookup"><span data-stu-id="e286d-327">INTERVAL DAY tooSECOND</span></span> |<span data-ttu-id="e286d-328">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e286d-328">TimeSpan</span></span> |
| <span data-ttu-id="e286d-329">UZUN</span><span class="sxs-lookup"><span data-stu-id="e286d-329">LONG</span></span> |<span data-ttu-id="e286d-330">Dize</span><span class="sxs-lookup"><span data-stu-id="e286d-330">String</span></span> |
| <span data-ttu-id="e286d-331">UZUN HAM</span><span class="sxs-lookup"><span data-stu-id="e286d-331">LONG RAW</span></span> |<span data-ttu-id="e286d-332">Byte]</span><span class="sxs-lookup"><span data-stu-id="e286d-332">Byte[]</span></span> |
| <span data-ttu-id="e286d-333">NCHAR</span><span class="sxs-lookup"><span data-stu-id="e286d-333">NCHAR</span></span> |<span data-ttu-id="e286d-334">Dize</span><span class="sxs-lookup"><span data-stu-id="e286d-334">String</span></span> |
| <span data-ttu-id="e286d-335">NCLOB</span><span class="sxs-lookup"><span data-stu-id="e286d-335">NCLOB</span></span> |<span data-ttu-id="e286d-336">Dize</span><span class="sxs-lookup"><span data-stu-id="e286d-336">String</span></span> |
| <span data-ttu-id="e286d-337">SAYI</span><span class="sxs-lookup"><span data-stu-id="e286d-337">NUMBER</span></span> |<span data-ttu-id="e286d-338">Ondalık, dize (varsa precision > 28)</span><span class="sxs-lookup"><span data-stu-id="e286d-338">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="e286d-339">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="e286d-339">NVARCHAR2</span></span> |<span data-ttu-id="e286d-340">Dize</span><span class="sxs-lookup"><span data-stu-id="e286d-340">String</span></span> |
| <span data-ttu-id="e286d-341">HAM</span><span class="sxs-lookup"><span data-stu-id="e286d-341">RAW</span></span> |<span data-ttu-id="e286d-342">Byte]</span><span class="sxs-lookup"><span data-stu-id="e286d-342">Byte[]</span></span> |
| <span data-ttu-id="e286d-343">SATIR KİMLİĞİ</span><span class="sxs-lookup"><span data-stu-id="e286d-343">ROWID</span></span> |<span data-ttu-id="e286d-344">Dize</span><span class="sxs-lookup"><span data-stu-id="e286d-344">String</span></span> |
| <span data-ttu-id="e286d-345">ZAMAN DAMGASI</span><span class="sxs-lookup"><span data-stu-id="e286d-345">TIMESTAMP</span></span> |<span data-ttu-id="e286d-346">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="e286d-346">DateTime</span></span> |
| <span data-ttu-id="e286d-347">YEREL SAAT DİLİMİ ZAMAN DAMGASI</span><span class="sxs-lookup"><span data-stu-id="e286d-347">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="e286d-348">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="e286d-348">DateTime</span></span> |
| <span data-ttu-id="e286d-349">SAAT DİLİMİ ZAMAN DAMGASI</span><span class="sxs-lookup"><span data-stu-id="e286d-349">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="e286d-350">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="e286d-350">DateTime</span></span> |
| <span data-ttu-id="e286d-351">İŞARETSİZ TAMSAYI</span><span class="sxs-lookup"><span data-stu-id="e286d-351">UNSIGNED INTEGER</span></span> |<span data-ttu-id="e286d-352">Sayı</span><span class="sxs-lookup"><span data-stu-id="e286d-352">Number</span></span> |
| <span data-ttu-id="e286d-353">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="e286d-353">VARCHAR2</span></span> |<span data-ttu-id="e286d-354">Dize</span><span class="sxs-lookup"><span data-stu-id="e286d-354">String</span></span> |
| <span data-ttu-id="e286d-355">XML</span><span class="sxs-lookup"><span data-stu-id="e286d-355">XML</span></span> |<span data-ttu-id="e286d-356">Dize</span><span class="sxs-lookup"><span data-stu-id="e286d-356">String</span></span> |

> [!NOTE]
> <span data-ttu-id="e286d-357">Veri türü **ARALIĞI yıl tooMONTH** ve **ARALIĞI gün tooSECOND** Microsoft sürücüsü kullanılırken desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="e286d-357">Data type **INTERVAL YEAR tooMONTH** and **INTERVAL DAY tooSECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="e286d-358">Kaynak toosink sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="e286d-358">Map source toosink columns</span></span>
<span data-ttu-id="e286d-359">Kaynak veri kümesi toocolumns havuz kümesindeki eşleme sütunlarında hakkında toolearn bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="e286d-359">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="e286d-360">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="e286d-360">Repeatable read from relational sources</span></span>
<span data-ttu-id="e286d-361">İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları.</span><span class="sxs-lookup"><span data-stu-id="e286d-361">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="e286d-362">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e286d-362">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="e286d-363">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e286d-363">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="e286d-364">Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e286d-364">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="e286d-365">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="e286d-365">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="e286d-366">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="e286d-366">Performance and Tuning</span></span>
<span data-ttu-id="e286d-367">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="e286d-367">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
