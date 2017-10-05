---
title: Veri kopyalama/Data Factory kullanarak Oracle | Microsoft Docs
description: "Öğesine/öğesinden veritabanını Azure Data Factory kullanarak şirket içi Oracle veri kopyalama öğrenin."
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
ms.openlocfilehash: bb6af719fe6f1a30c5933ce4342a4c0c072f3ff4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="8a3dc-103">Öğesine/öğesinden Azure Data Factory kullanarak şirket içi Oracle veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="8a3dc-103">Copy data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="8a3dc-104">Bu makalede kopya etkinliği Azure Data Factory'de bir şirket içi Oracle veritabanından/gelen verileri taşımak için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="8a3dc-105">Derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) kopyalama etkinliği ile veri taşıma için genel bir bakış sunar makalesi.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="8a3dc-106">Desteklenen senaryolar</span><span class="sxs-lookup"><span data-stu-id="8a3dc-106">Supported scenarios</span></span>
<span data-ttu-id="8a3dc-107">Veri kopyalama **bir Oracle veritabanından** aşağıdaki veri depolar:</span><span class="sxs-lookup"><span data-stu-id="8a3dc-107">You can copy data **from an Oracle database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="8a3dc-108">Aşağıdaki veri depolarına verileri kopyalayabilirsiniz **bir Oracle veritabanına**:</span><span class="sxs-lookup"><span data-stu-id="8a3dc-108">You can copy data from the following data stores **to an Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="8a3dc-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8a3dc-109">Prerequisites</span></span>
<span data-ttu-id="8a3dc-110">Data Factory veri yönetimi ağ geçidi kullanarak şirket içi Oracle kaynaklarına bağlanma destekler.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-110">Data Factory supports connecting to on-premises Oracle sources using the Data Management Gateway.</span></span> <span data-ttu-id="8a3dc-111">Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) veri yönetimi ağ geçidi hakkında bilgi edinmek için makale ve [buluta şirket içinden veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) ağ geçidi kurun veri ardışık ayarlamak adım adım yönergeler için makalenin verileri taşıyın.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article to learn about Data Management Gateway and [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="8a3dc-112">Bir Azure Iaas sanal Oracle barındırılan olsa bile ağ geçidi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-112">Gateway is required even if the Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="8a3dc-113">Ağ geçidi veritabanına bağlanıp sürece veri deposu olarak aynı Iaas VM veya farklı bir VM ağ geçidi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="8a3dc-114">Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="8a3dc-115">Desteklenen sürümleri ve yükleme</span><span class="sxs-lookup"><span data-stu-id="8a3dc-115">Supported versions and installation</span></span>
<span data-ttu-id="8a3dc-116">Bu Oracle bağlayıcı sürücülerin iki sürümlerini destekler:</span><span class="sxs-lookup"><span data-stu-id="8a3dc-116">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="8a3dc-117">**(Önerilen) Oracle için Microsoft sürücüsü**: veri yönetimi ağ geçidi sürümü 2.7, sürücü Oracle otomatik olarak ağ geçidi ile birlikte yüklenir, ayrıca gerek kalmaması için işlemek için sürücü Microsoft başlayarak Oracle bağlantı kurar ve bu sürücü kullanarak daha iyi kopyalama performansını da karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-117">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with the gateway, so you don't need to additionally handle the driver in order to establish connectivity to Oracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="8a3dc-118">Oracle sürümleri veritabanları desteklenir:</span><span class="sxs-lookup"><span data-stu-id="8a3dc-118">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="8a3dc-119">Oracle 12c R1 (12,1)</span><span class="sxs-lookup"><span data-stu-id="8a3dc-119">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="8a3dc-120">Oracle 11g R1, R2 (11.1, 11.2)</span><span class="sxs-lookup"><span data-stu-id="8a3dc-120">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="8a3dc-121">Oracle 10g R1, R2 (10,1, 10.2)</span><span class="sxs-lookup"><span data-stu-id="8a3dc-121">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="8a3dc-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span><span class="sxs-lookup"><span data-stu-id="8a3dc-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="8a3dc-123">Oracle 8i R3 (8.1.7)</span><span class="sxs-lookup"><span data-stu-id="8a3dc-123">Oracle 8i R3 (8.1.7)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8a3dc-124">Şu anda Oracle için Microsoft sürücüsü yalnızca Oracle ancak için Oracle yazılamıyor veri kopyalamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-124">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing to Oracle.</span></span> <span data-ttu-id="8a3dc-125">Ve veri yönetimi ağ geçidi tanılama sekmesinde test bağlantısı özelliği bu sürücüyü desteklemiyor not edin.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-125">And note the test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="8a3dc-126">Alternatif olarak, bağlantıyı doğrulamak için kopyalama Sihirbazı'nı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-126">Alternatively, you can use the copy wizard to validate the connectivity.</span></span>
>

- <span data-ttu-id="8a3dc-127">**.NET için Oracle veri sağlayıcısı:**  /Oracle veri kopyalamak için Oracle veri sağlayıcısı kullanmayı da seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-127">**Oracle Data Provider for .NET:** you can also choose to use Oracle Data Provider to copy data from/to Oracle.</span></span> <span data-ttu-id="8a3dc-128">Bu bileşen dahil [için Oracle veri erişim bileşenleri Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8a3dc-128">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="8a3dc-129">Uygun sürüm (32/64 bit), ağ geçidinin yüklü olduğu makineye yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-129">Install the appropriate version (32/64 bit) on the machine where the gateway is installed.</span></span> <span data-ttu-id="8a3dc-130">[Oracle veri sağlayıcısı .NET 12,1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) Oracle veritabanına 10 g sürüm 2 veya sonrasını erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access to Oracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="8a3dc-131">"XCopy yükleme" seçerseniz, readme.htm adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-131">If you choose “XCopy Installation”, follow steps in the readme.htm.</span></span> <span data-ttu-id="8a3dc-132">Kullanıcı Arabirimi (olmayan-XCopy biri) ile yükleyici seçtiğiniz öneririz.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-132">We recommend you choose the installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="8a3dc-133">Sağlayıcı yüklendikten sonra **yeniden** Hizmetleri uygulaması (veya) veri yönetimi ağ geçidi Yapılandırma Yöneticisi kullanarak makinenizde veri yönetimi ağ geçidi ana bilgisayar hizmeti.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-133">After installing the provider, **restart** the Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="8a3dc-134">Kopyalama işlem hattını yazmak için kopyalama Sihirbazı'nı kullanırsanız sürücü türünü otomatik olarak belirlenir.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-134">If you use copy wizard to author the copy pipeline, the driver type will be auto-determined.</span></span> <span data-ttu-id="8a3dc-135">Microsoft sürücüsü, ağ geçidi sürümü 2.7 düşük olduğu veya Oracle havuz olarak seçtiğiniz sürece varsayılan olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-135">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="8a3dc-136">Başlarken</span><span class="sxs-lookup"><span data-stu-id="8a3dc-136">Getting started</span></span>
<span data-ttu-id="8a3dc-137">Farklı araçlar/API'lerini kullanarak bir şirket içi Oracle veritabanından/gelen verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-137">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="8a3dc-138">Bir işlem hattı oluşturmak için en kolay yolu kullanmaktır **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-138">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="8a3dc-139">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) veri kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-139">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="8a3dc-140">Bir işlem hattı oluşturmak için aşağıdaki araçları kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu**, **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-140">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="8a3dc-141">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-141">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="8a3dc-142">Araçlar ya da API'leri kullanıp bir havuz veri deposu için bir kaynak veri deposundan verileri taşır bir ardışık düzen oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="8a3dc-142">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="8a3dc-143">Oluşturma bir **veri fabrikası**.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-143">Create a **data factory**.</span></span> <span data-ttu-id="8a3dc-144">Veri Fabrikası bir veya daha fazla ardışık düzen içerebilir.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-144">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="8a3dc-145">Oluşturma **bağlantılı Hizmetleri** girdi ve çıktı verilerini bağlamak için veri fabrikanıza depolar.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-145">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="8a3dc-146">Örneğin, bir Azure blob depolama alanına bir Oralce veritabanından veri kopyalıyorsanız, Oracle veritabanı ve Azure depolama hesabı veri fabrikanıza bağlamak için iki bağlı hizmet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-146">For example, if you are copying data from an Oralce database to an Azure blob storage, you create two linked services to link your Oracle database and Azure storage account to your data factory.</span></span> <span data-ttu-id="8a3dc-147">Oracle için özel bağlantılı hizmet özellikleri için bkz: [bağlantılı hizmet özellikleri](#linked-service-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-147">For linked service properties that are specific to Oracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="8a3dc-148">Oluşturma **veri kümeleri** kopyalama işlemi için girdi ve çıktı verilerini temsil etmek için.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-148">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="8a3dc-149">Son adımda bahsedilen örnekte, Oracle veritabanınız giriş verileri içeren tablo belirtmek için bir veri kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-149">In the example mentioned in the last step, you create a dataset to specify the table in your Oracle database that contains the input data.</span></span> <span data-ttu-id="8a3dc-150">Ve blob kapsayıcısında ve Oracle veritabanından kopyalanan verileri tutan klasör belirtmek için başka bir veri kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-150">And, you create another dataset to specify the blob container and the folder that holds the data copied from the Oracle database.</span></span> <span data-ttu-id="8a3dc-151">Oracle için özel veri kümesi özellikleri için bkz: [veri kümesi özellikleri](#dataset-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-151">For dataset properties that are specific to Oracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="8a3dc-152">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-152">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="8a3dc-153">Daha önce bahsedilen örnekte OracleSource bir kaynak ve BlobSink havuzu olarak kopya etkinliği için kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-153">In the example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="8a3dc-154">Oracle veritabanına Azure Blob depolama alanından kopyalıyorsanız benzer şekilde, BlobSource ve OracleSink kopyalama etkinliği kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-154">Similarly, if you are copying from Azure Blob Storage to Oracle Database, you use BlobSource and OracleSink in the copy activity.</span></span> <span data-ttu-id="8a3dc-155">Oracle veritabanına belirli kopyalama etkinliği özellikleri için bkz: [kopyalama etkinliği özellikleri](#copy-activity-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-155">For copy activity properties that are specific to Oracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="8a3dc-156">Bir veri deposu bir kaynak veya bir havuz nasıl kullanılacağı hakkında daha fazla bilgi için önceki bölümde, veri deposu için bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-156">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="8a3dc-157">Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-157">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="8a3dc-158">Araçlar/API'leri (dışında .NET API'si) kullandığınızda, JSON biçimini kullanarak bu Data Factory varlıklarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-158">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="8a3dc-159">/ Bir şirket içi Oracle veritabanından veri kopyalamak için kullanılan Data Factory varlıkları için JSON tanımlarıyla örnekleri için bkz: [JSON örnekler](#json-examples-for-copying-data-to-and-from-oracle-database) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-159">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="8a3dc-160">Aşağıdaki bölümler, Data Factory varlıklarını tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılı bilgi sağlar:</span><span class="sxs-lookup"><span data-stu-id="8a3dc-160">The following sections provide details about JSON properties that are used to define Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="8a3dc-161">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="8a3dc-161">Linked service properties</span></span>
<span data-ttu-id="8a3dc-162">Aşağıdaki tabloda, JSON öğeleri Oracle bağlantılı hizmete özgü açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-162">The following table provides description for JSON elements specific to Oracle linked service.</span></span>

| <span data-ttu-id="8a3dc-163">Özellik</span><span class="sxs-lookup"><span data-stu-id="8a3dc-163">Property</span></span> | <span data-ttu-id="8a3dc-164">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8a3dc-164">Description</span></span> | <span data-ttu-id="8a3dc-165">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8a3dc-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8a3dc-166">type</span><span class="sxs-lookup"><span data-stu-id="8a3dc-166">type</span></span> |<span data-ttu-id="8a3dc-167">Type özelliği ayarlanmalıdır: **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="8a3dc-167">The type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="8a3dc-168">Evet</span><span class="sxs-lookup"><span data-stu-id="8a3dc-168">Yes</span></span> |
| <span data-ttu-id="8a3dc-169">driverType</span><span class="sxs-lookup"><span data-stu-id="8a3dc-169">driverType</span></span> | <span data-ttu-id="8a3dc-170">Hangi sürücünün/Oracle veritabanına veri kopyalamak için kullanılacağını belirtin.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-170">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="8a3dc-171">İzin verilen değerler **Microsoft** veya **ODP** (varsayılan).</span><span class="sxs-lookup"><span data-stu-id="8a3dc-171">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="8a3dc-172">Bkz: [desteklenen sürümü ve yükleme](#supported-versions-and-installation) sürücü ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-172">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="8a3dc-173">Hayır</span><span class="sxs-lookup"><span data-stu-id="8a3dc-173">No</span></span> |
| <span data-ttu-id="8a3dc-174">connectionString</span><span class="sxs-lookup"><span data-stu-id="8a3dc-174">connectionString</span></span> | <span data-ttu-id="8a3dc-175">ConnectionString özelliği için Oracle veritabanı örneğine bağlanmak için gereken bilgileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-175">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="8a3dc-176">Evet</span><span class="sxs-lookup"><span data-stu-id="8a3dc-176">Yes</span></span> |
| <span data-ttu-id="8a3dc-177">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8a3dc-177">gatewayName</span></span> | <span data-ttu-id="8a3dc-178">Ağ geçidinin adı, şirket içi Oracle sunucusuna bağlanmak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="8a3dc-178">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="8a3dc-179">Evet</span><span class="sxs-lookup"><span data-stu-id="8a3dc-179">Yes</span></span> |

<span data-ttu-id="8a3dc-180">**Örnek: Microsoft sürücüsü kullanma:**</span><span class="sxs-lookup"><span data-stu-id="8a3dc-180">**Example: using Microsoft driver:**</span></span>
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

<span data-ttu-id="8a3dc-181">**Örnek: ODP sürücü kullanma**</span><span class="sxs-lookup"><span data-stu-id="8a3dc-181">**Example: using ODP driver**</span></span>

<span data-ttu-id="8a3dc-182">Başvurmak [bu site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) izin verilen biçimler için.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-182">Refer to [this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for the allowed formats.</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="8a3dc-183">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="8a3dc-183">Dataset properties</span></span>
<span data-ttu-id="8a3dc-184">Bölümler & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-184">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="8a3dc-185">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Oracle, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-185">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="8a3dc-186">TypeProperties bölümü dataset her tür için farklıdır ve verilerin veri deposunda konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-186">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="8a3dc-187">Veri kümesi için typeProperties bölüm türü OracleTable aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="8a3dc-187">The typeProperties section for the dataset of type OracleTable has the following properties:</span></span>

| <span data-ttu-id="8a3dc-188">Özellik</span><span class="sxs-lookup"><span data-stu-id="8a3dc-188">Property</span></span> | <span data-ttu-id="8a3dc-189">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8a3dc-189">Description</span></span> | <span data-ttu-id="8a3dc-190">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8a3dc-190">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8a3dc-191">tableName</span><span class="sxs-lookup"><span data-stu-id="8a3dc-191">tableName</span></span> |<span data-ttu-id="8a3dc-192">Oracle veritabanında bağlantılı hizmet başvurduğu tablonun adı.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-192">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="8a3dc-193">Hayır (varsa **oracleReaderQuery** , **OracleSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="8a3dc-193">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="8a3dc-194">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="8a3dc-194">Copy activity properties</span></span>
<span data-ttu-id="8a3dc-195">Bölümler & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz: [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-195">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="8a3dc-196">Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-196">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="8a3dc-197">Kopyalama etkinliği yalnızca bir girdi alır ve tek bir çıktı üretir.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-197">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="8a3dc-198">Oysa etkinliğin typeProperties bölümündeki özellikler her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-198">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="8a3dc-199">Kopya etkinliği için bunlar türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-199">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="8a3dc-200">OracleSource</span><span class="sxs-lookup"><span data-stu-id="8a3dc-200">OracleSource</span></span>
<span data-ttu-id="8a3dc-201">Kopyalama etkinliğinde kaynak türü olduğunda **OracleSource** aşağıdaki özellikler mevcuttur **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="8a3dc-201">In Copy activity, when the source is of type **OracleSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="8a3dc-202">Özellik</span><span class="sxs-lookup"><span data-stu-id="8a3dc-202">Property</span></span> | <span data-ttu-id="8a3dc-203">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8a3dc-203">Description</span></span> | <span data-ttu-id="8a3dc-204">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="8a3dc-204">Allowed values</span></span> | <span data-ttu-id="8a3dc-205">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8a3dc-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8a3dc-206">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="8a3dc-206">oracleReaderQuery</span></span> |<span data-ttu-id="8a3dc-207">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-207">Use the custom query to read data.</span></span> |<span data-ttu-id="8a3dc-208">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-208">SQL query string.</span></span> <span data-ttu-id="8a3dc-209">Örneğin: seçin * from MyTable</span><span class="sxs-lookup"><span data-stu-id="8a3dc-209">For example: select * from MyTable</span></span> <br/><br/><span data-ttu-id="8a3dc-210">Belirtilmezse, yürütülen SQL deyimi: seçin * from MyTable</span><span class="sxs-lookup"><span data-stu-id="8a3dc-210">If not specified, the SQL statement that is executed: select * from MyTable</span></span> |<span data-ttu-id="8a3dc-211">Hayır (varsa **tableName** , **dataset** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="8a3dc-211">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="8a3dc-212">OracleSink</span><span class="sxs-lookup"><span data-stu-id="8a3dc-212">OracleSink</span></span>
<span data-ttu-id="8a3dc-213">**OracleSink** aşağıdaki özellikleri destekler:</span><span class="sxs-lookup"><span data-stu-id="8a3dc-213">**OracleSink** supports the following properties:</span></span>

| <span data-ttu-id="8a3dc-214">Özellik</span><span class="sxs-lookup"><span data-stu-id="8a3dc-214">Property</span></span> | <span data-ttu-id="8a3dc-215">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8a3dc-215">Description</span></span> | <span data-ttu-id="8a3dc-216">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="8a3dc-216">Allowed values</span></span> | <span data-ttu-id="8a3dc-217">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8a3dc-217">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8a3dc-218">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="8a3dc-218">writeBatchTimeout</span></span> |<span data-ttu-id="8a3dc-219">Toplu ekleme işlemi zaman aşımına uğramadan önce tamamlamak bir süre bekleyin.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-219">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="8a3dc-220">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="8a3dc-220">timespan</span></span><br/><br/> <span data-ttu-id="8a3dc-221">Örnek: 00:30:00 (30 dakika).</span><span class="sxs-lookup"><span data-stu-id="8a3dc-221">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="8a3dc-222">Hayır</span><span class="sxs-lookup"><span data-stu-id="8a3dc-222">No</span></span> |
| <span data-ttu-id="8a3dc-223">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="8a3dc-223">writeBatchSize</span></span> |<span data-ttu-id="8a3dc-224">Arabellek boyutu writeBatchSize ulaştığında veri SQL tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-224">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="8a3dc-225">Tamsayı (satır sayısı)</span><span class="sxs-lookup"><span data-stu-id="8a3dc-225">Integer (number of rows)</span></span> |<span data-ttu-id="8a3dc-226">Hayır (varsayılan: 100)</span><span class="sxs-lookup"><span data-stu-id="8a3dc-226">No (default: 100)</span></span> |
| <span data-ttu-id="8a3dc-227">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="8a3dc-227">sqlWriterCleanupScript</span></span> |<span data-ttu-id="8a3dc-228">Belirli bir dilimle verilerinin temizlenmesini şekilde yürütmek kopyalama etkinliği için bir sorgu belirtin.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-228">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="8a3dc-229">Sorgu bildirimi.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-229">A query statement.</span></span> |<span data-ttu-id="8a3dc-230">Hayır</span><span class="sxs-lookup"><span data-stu-id="8a3dc-230">No</span></span> |
| <span data-ttu-id="8a3dc-231">Sliceıdentifiercolumnname</span><span class="sxs-lookup"><span data-stu-id="8a3dc-231">sliceIdentifierColumnName</span></span> |<span data-ttu-id="8a3dc-232">Kopyalama etkinliği'nin ne zaman yeniden çalıştırılacağını belirli bir dilim verileri temizlemek için kullanılan otomatik dilim tanımlayıcı doldurmak için sütun adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-232">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="8a3dc-233">Binary(32) veri türüne sahip bir sütunun sütun adı.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="8a3dc-234">Hayır</span><span class="sxs-lookup"><span data-stu-id="8a3dc-234">No</span></span> |

## <a name="json-examples-for-copying-data-to-and-from-oracle-database"></a><span data-ttu-id="8a3dc-235">JSON örnekleri ve Oracle veritabanından veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="8a3dc-235">JSON examples for copying data to and from Oracle database</span></span>
<span data-ttu-id="8a3dc-236">Aşağıdaki örneği kullanarak bir işlem hattı oluşturmak için kullanabileceğiniz örnek JSON tanımları sağlar, [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8a3dc-236">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="8a3dc-237">Bunlar, Oracle veritabanından için/Azure Blob Depolama / için verileri kopyalamak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-237">They show how to copy data from/to an Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="8a3dc-238">Ancak, veri herhangi belirtildiği havuzlarını kopyalanabilir [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kopya etkinliği Azure Data Factory kullanarak.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-238">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-to-azure-blob"></a><span data-ttu-id="8a3dc-239">Örnek: verileri Oracle'dan Azure Blob kopyalama</span><span class="sxs-lookup"><span data-stu-id="8a3dc-239">Example: Copy data from Oracle to Azure Blob</span></span>

<span data-ttu-id="8a3dc-240">Örnek aşağıdaki data factory varlıklarını sahiptir:</span><span class="sxs-lookup"><span data-stu-id="8a3dc-240">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="8a3dc-241">Bağlı hizmet türü [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8a3dc-241">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="8a3dc-242">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8a3dc-242">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="8a3dc-243">Bir giriş [dataset](data-factory-create-datasets.md) türü [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8a3dc-243">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="8a3dc-244">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8a3dc-244">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="8a3dc-245">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) kaynağı olarak ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) havuz olarak.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-245">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="8a3dc-246">Örnek verileri şirket içi Oracle veritabanına bir tablodaki bir blobu saatlik kopyalar.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-246">The sample copies data from a table in an on-premises Oracle database to a blob hourly.</span></span> <span data-ttu-id="8a3dc-247">Aşağıdaki örnekte kullanılan çeşitli özellikler hakkında daha fazla bilgi için örnekleri aşağıdaki bölümlerde belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-247">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="8a3dc-248">**Oracle bağlantılı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="8a3dc-248">**Oracle linked service:**</span></span>

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

<span data-ttu-id="8a3dc-249">**Azure Blob storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="8a3dc-249">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="8a3dc-250">**Oracle girdi veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="8a3dc-250">**Oracle input dataset:**</span></span>

<span data-ttu-id="8a3dc-251">Örnek, Oracle tablo "MyTable" oluşturulur ve zaman serisi veri için "timestampcolumn" adlı bir sütun içerdiği varsayar.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-251">The sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="8a3dc-252">"Dış" ayarı: "true" bildirir Data Factory hizmetinin veri kümesi data factory dış ve veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-252">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="8a3dc-253">**Azure Blob dataset çıktı:**</span><span class="sxs-lookup"><span data-stu-id="8a3dc-253">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="8a3dc-254">Veri her saat yeni bir bloba yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="8a3dc-254">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="8a3dc-255">Blob klasör yolu ve dosya adı dinamik olarak değerlendirilir işleniyor dilim başlangıç zamanı temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-255">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="8a3dc-256">Klasör yolu yıl, ay, gün ve saat bölümleri başlangıç saatini kullanır.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-256">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="8a3dc-257">**Kopyalama etkinliği ile kanal:**</span><span class="sxs-lookup"><span data-stu-id="8a3dc-257">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="8a3dc-258">Ardışık Düzen giriş ve çıkış veri kümeleri kullanmak üzere yapılandırılmış ve saatte bir çalışacak şekilde zamanlanmış bir kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-258">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="8a3dc-259">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **OracleSource** ve **havuz** türü ayarlanmış **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-259">In the pipeline JSON definition, the **source** type is set to **OracleSource** and **sink** type is set to **BlobSink**.</span></span>  <span data-ttu-id="8a3dc-260">Belirtilen SQL sorgusu **oracleReaderQuery** özelliği veri kopyalamak için son bir saat içindeki seçer.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-260">The SQL query specified with **oracleReaderQuery** property selects the data in the past hour to copy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-to-oracle"></a><span data-ttu-id="8a3dc-261">Örnek: verileri Azure Blob'tan için Oracle kopyalayın</span><span class="sxs-lookup"><span data-stu-id="8a3dc-261">Example: Copy data from Azure Blob to Oracle</span></span>
<span data-ttu-id="8a3dc-262">Bu örnek bir Azure Blob depolama alanından bir şirket içi Oracle veritabanına veri kopyalamak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-262">This sample shows how to copy data from an Azure Blob Storage to an on-premises Oracle database.</span></span> <span data-ttu-id="8a3dc-263">Ancak, veriler kopyalanabilir **doğrudan** herhangi belirtildiği kaynakları [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kopya etkinliği Azure Data Factory kullanarak.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-263">However, data can be copied **directly** from any of the sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="8a3dc-264">Örnek aşağıdaki data factory varlıklarını sahiptir:</span><span class="sxs-lookup"><span data-stu-id="8a3dc-264">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="8a3dc-265">Bağlı hizmet türü [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8a3dc-265">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="8a3dc-266">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8a3dc-266">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="8a3dc-267">Bir giriş [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8a3dc-267">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="8a3dc-268">Bir çıkış [dataset](data-factory-create-datasets.md) türü [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8a3dc-268">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="8a3dc-269">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) kaynağı olarak [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) havuz olarak.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-269">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="8a3dc-270">Örnek verileri blob üzerinden şirket içi Oracle veritabanına tablosunda her saat kopyalar.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-270">The sample copies data from a blob to a table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="8a3dc-271">Aşağıdaki örnekte kullanılan çeşitli özellikler hakkında daha fazla bilgi için örnekleri aşağıdaki bölümlerde belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-271">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="8a3dc-272">**Oracle bağlantılı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="8a3dc-272">**Oracle linked service:**</span></span>
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

<span data-ttu-id="8a3dc-273">**Azure Blob storage bağlı hizmeti:**</span><span class="sxs-lookup"><span data-stu-id="8a3dc-273">**Azure Blob storage linked service:**</span></span>
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

<span data-ttu-id="8a3dc-274">**Azure Blob girdi veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="8a3dc-274">**Azure Blob input dataset**</span></span>

<span data-ttu-id="8a3dc-275">Veri toplanma yeni blob üzerinden saatte (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="8a3dc-275">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="8a3dc-276">Blob klasör yolu ve dosya adı dinamik olarak değerlendirilir işleniyor dilim başlangıç zamanı temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-276">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="8a3dc-277">Klasör yolu yıl, ay ve gün kısmını başlangıç saati ve dosya adı başlangıç zamanı saat bölümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-277">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="8a3dc-278">"dış": "true" ayarı Bu tablo veri fabrikası dış ve veri fabrikasında bir etkinlik tarafından üretilen değil Data Factory hizmetinin sizi bilgilendirir.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-278">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="8a3dc-279">**Oracle çıktı veri kümesi:**</span><span class="sxs-lookup"><span data-stu-id="8a3dc-279">**Oracle output dataset:**</span></span>

<span data-ttu-id="8a3dc-280">Örnek bir tablo "MyTable" Oracle oluşturdunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-280">The sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="8a3dc-281">Blob CSV dosyasında içerecek şekilde beklediğiniz gibi tablo Oracle ile aynı sayıda sütun oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-281">Create the table in Oracle with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="8a3dc-282">Yeni satırlar tabloya saatte eklenir.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-282">New rows are added to the table every hour.</span></span>

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

<span data-ttu-id="8a3dc-283">**Kopyalama etkinliği ile kanal:**</span><span class="sxs-lookup"><span data-stu-id="8a3dc-283">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="8a3dc-284">Ardışık Düzen giriş ve çıkış veri kümeleri kullanmak üzere yapılandırıldığı ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-284">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="8a3dc-285">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **BlobSource** ve **havuz** türü ayarlanmış **OracleSink**.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-285">In the pipeline JSON definition, the **source** type is set to **BlobSource** and the **sink** type is set to **OracleSink**.</span></span>  

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


## <a name="troubleshooting-tips"></a><span data-ttu-id="8a3dc-286">Sorun giderme ipuçları</span><span class="sxs-lookup"><span data-stu-id="8a3dc-286">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="8a3dc-287">Sorun 1: .NET Framework veri sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="8a3dc-287">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="8a3dc-288">Aşağıdaki bakın **hata iletisi**:</span><span class="sxs-lookup"><span data-stu-id="8a3dc-288">You see the following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable to find the requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="8a3dc-289">**Olası nedenler:**</span><span class="sxs-lookup"><span data-stu-id="8a3dc-289">**Possible causes:**</span></span>

1. <span data-ttu-id="8a3dc-290">Oracle için .NET Framework veri sağlayıcısı yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-290">The .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="8a3dc-291">Oracle için .NET Framework veri sağlayıcısı için .NET Framework 2.0 yüklendi ve .NET Framework 4.0 klasörlerde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-291">The .NET Framework Data Provider for Oracle was installed to .NET Framework 2.0 and is not found in the .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="8a3dc-292">**Çözümleme/geçici çözüm:**</span><span class="sxs-lookup"><span data-stu-id="8a3dc-292">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="8a3dc-293">Oracle, .NET sağlayıcısı yüklemediyseniz [yüklemek](http://www.oracle.com/technetwork/topics/dotnet/downloads/) ve senaryo yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-293">If you haven't installed the .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry the scenario.</span></span>
2. <span data-ttu-id="8a3dc-294">Sağlayıcı yüklendikten sonra bile hata iletisi alırsanız, aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="8a3dc-294">If you get the error message even after installing the provider, do the following steps:</span></span>
   1. <span data-ttu-id="8a3dc-295">Makine yapılandırma .NET 2.0 klasöründen açın: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-295">Open machine config of .NET 2.0 from the folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="8a3dc-296">Arama **.NET için Oracle veri sağlayıcısı**, ve altında aşağıdaki örnekte gösterildiği gibi bir giriş bulamadı olmalıdır **system.data** -> **DbProviderFactories**: "<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description=".NET için oracle veri sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="8a3dc-296">Search for **Oracle Data Provider for .NET**, and you should be able to find an entry as shown in the following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="8a3dc-297">”</span><span class="sxs-lookup"><span data-stu-id="8a3dc-297">”</span></span>
3. <span data-ttu-id="8a3dc-298">Machine.config dosyasının aşağıdaki v4.0 klasörde bu girdiyi kopyalayın: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config ve değişiklik 4.xxx.x.x sürüme.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-298">Copy this entry to the machine.config file in the following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change the version to 4.xxx.x.x.</span></span>
4. <span data-ttu-id="8a3dc-299">"< ODP.NET yüklü yolu > \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll" Genel Derleme Önbelleği'ne (GAC) çalıştırarak yükleyin `gacutil /i [provider path]`. ## sorun giderme ipuçları</span><span class="sxs-lookup"><span data-stu-id="8a3dc-299">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into the global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="8a3dc-300">Sorun 2: datetime biçimlendirme</span><span class="sxs-lookup"><span data-stu-id="8a3dc-300">Problem 2: datetime formatting</span></span>

<span data-ttu-id="8a3dc-301">Aşağıdaki bakın **hata iletisi**:</span><span class="sxs-lookup"><span data-stu-id="8a3dc-301">You see the following **error message**:</span></span>

    Message=Operation failed in Oracle Database with the following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="8a3dc-302">**Çözümleme/geçici çözüm:**</span><span class="sxs-lookup"><span data-stu-id="8a3dc-302">**Resolution/Workaround:**</span></span>

<span data-ttu-id="8a3dc-303">Sorgu dizesi (to_date işlevi kullanılarak) aşağıdaki örnekte gösterildiği gibi tarihleri, Oracle veritabanınızı nasıl yapılandırıldığına göre kopyalama etkinliğinde ayarlamanız gerekebilir:</span><span class="sxs-lookup"><span data-stu-id="8a3dc-303">You may need to adjust the query string in your copy activity based on how dates are configured in your Oracle database, as shown in the following sample (using the to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="8a3dc-304">Oracle için tür eşlemesi</span><span class="sxs-lookup"><span data-stu-id="8a3dc-304">Type mapping for Oracle</span></span>
<span data-ttu-id="8a3dc-305">Bölümünde belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale kopyalama etkinliği aşağıdaki 2 adımlı yaklaşımı türleriyle havuz için kaynak türünden otomatik tür dönüşümleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="8a3dc-305">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="8a3dc-306">Yerel kaynak türlerinden .NET türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="8a3dc-306">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="8a3dc-307">.NET türünden yerel havuz türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="8a3dc-307">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="8a3dc-308">Verileri Oracle'dan taşırken, aşağıdaki eşlemelerini Oracle veri türünden .NET türü ve tersi yönde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-308">When moving data from Oracle, the following mappings are used from Oracle data type to .NET type and vice versa.</span></span>

| <span data-ttu-id="8a3dc-309">Oracle veri türü</span><span class="sxs-lookup"><span data-stu-id="8a3dc-309">Oracle data type</span></span> | <span data-ttu-id="8a3dc-310">.NET framework veri türü</span><span class="sxs-lookup"><span data-stu-id="8a3dc-310">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="8a3dc-311">BDOSYA</span><span class="sxs-lookup"><span data-stu-id="8a3dc-311">BFILE</span></span> |<span data-ttu-id="8a3dc-312">Byte]</span><span class="sxs-lookup"><span data-stu-id="8a3dc-312">Byte[]</span></span> |
| <span data-ttu-id="8a3dc-313">BLOB</span><span class="sxs-lookup"><span data-stu-id="8a3dc-313">BLOB</span></span> |<span data-ttu-id="8a3dc-314">Byte]</span><span class="sxs-lookup"><span data-stu-id="8a3dc-314">Byte[]</span></span> |
| <span data-ttu-id="8a3dc-315">CHAR</span><span class="sxs-lookup"><span data-stu-id="8a3dc-315">CHAR</span></span> |<span data-ttu-id="8a3dc-316">Dize</span><span class="sxs-lookup"><span data-stu-id="8a3dc-316">String</span></span> |
| <span data-ttu-id="8a3dc-317">CLOB</span><span class="sxs-lookup"><span data-stu-id="8a3dc-317">CLOB</span></span> |<span data-ttu-id="8a3dc-318">Dize</span><span class="sxs-lookup"><span data-stu-id="8a3dc-318">String</span></span> |
| <span data-ttu-id="8a3dc-319">TARİH</span><span class="sxs-lookup"><span data-stu-id="8a3dc-319">DATE</span></span> |<span data-ttu-id="8a3dc-320">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="8a3dc-320">DateTime</span></span> |
| <span data-ttu-id="8a3dc-321">KAYAN NOKTA</span><span class="sxs-lookup"><span data-stu-id="8a3dc-321">FLOAT</span></span> |<span data-ttu-id="8a3dc-322">Ondalık, dize (varsa precision > 28)</span><span class="sxs-lookup"><span data-stu-id="8a3dc-322">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="8a3dc-323">TAMSAYI</span><span class="sxs-lookup"><span data-stu-id="8a3dc-323">INTEGER</span></span> |<span data-ttu-id="8a3dc-324">Ondalık, dize (varsa precision > 28)</span><span class="sxs-lookup"><span data-stu-id="8a3dc-324">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="8a3dc-325">ARALIĞI YIL AY İÇİN</span><span class="sxs-lookup"><span data-stu-id="8a3dc-325">INTERVAL YEAR TO MONTH</span></span> |<span data-ttu-id="8a3dc-326">Int32</span><span class="sxs-lookup"><span data-stu-id="8a3dc-326">Int32</span></span> |
| <span data-ttu-id="8a3dc-327">İKİNCİ GÜN ARALIĞI</span><span class="sxs-lookup"><span data-stu-id="8a3dc-327">INTERVAL DAY TO SECOND</span></span> |<span data-ttu-id="8a3dc-328">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="8a3dc-328">TimeSpan</span></span> |
| <span data-ttu-id="8a3dc-329">UZUN</span><span class="sxs-lookup"><span data-stu-id="8a3dc-329">LONG</span></span> |<span data-ttu-id="8a3dc-330">Dize</span><span class="sxs-lookup"><span data-stu-id="8a3dc-330">String</span></span> |
| <span data-ttu-id="8a3dc-331">UZUN HAM</span><span class="sxs-lookup"><span data-stu-id="8a3dc-331">LONG RAW</span></span> |<span data-ttu-id="8a3dc-332">Byte]</span><span class="sxs-lookup"><span data-stu-id="8a3dc-332">Byte[]</span></span> |
| <span data-ttu-id="8a3dc-333">NCHAR</span><span class="sxs-lookup"><span data-stu-id="8a3dc-333">NCHAR</span></span> |<span data-ttu-id="8a3dc-334">Dize</span><span class="sxs-lookup"><span data-stu-id="8a3dc-334">String</span></span> |
| <span data-ttu-id="8a3dc-335">NCLOB</span><span class="sxs-lookup"><span data-stu-id="8a3dc-335">NCLOB</span></span> |<span data-ttu-id="8a3dc-336">Dize</span><span class="sxs-lookup"><span data-stu-id="8a3dc-336">String</span></span> |
| <span data-ttu-id="8a3dc-337">SAYI</span><span class="sxs-lookup"><span data-stu-id="8a3dc-337">NUMBER</span></span> |<span data-ttu-id="8a3dc-338">Ondalık, dize (varsa precision > 28)</span><span class="sxs-lookup"><span data-stu-id="8a3dc-338">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="8a3dc-339">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="8a3dc-339">NVARCHAR2</span></span> |<span data-ttu-id="8a3dc-340">Dize</span><span class="sxs-lookup"><span data-stu-id="8a3dc-340">String</span></span> |
| <span data-ttu-id="8a3dc-341">HAM</span><span class="sxs-lookup"><span data-stu-id="8a3dc-341">RAW</span></span> |<span data-ttu-id="8a3dc-342">Byte]</span><span class="sxs-lookup"><span data-stu-id="8a3dc-342">Byte[]</span></span> |
| <span data-ttu-id="8a3dc-343">SATIR KİMLİĞİ</span><span class="sxs-lookup"><span data-stu-id="8a3dc-343">ROWID</span></span> |<span data-ttu-id="8a3dc-344">Dize</span><span class="sxs-lookup"><span data-stu-id="8a3dc-344">String</span></span> |
| <span data-ttu-id="8a3dc-345">ZAMAN DAMGASI</span><span class="sxs-lookup"><span data-stu-id="8a3dc-345">TIMESTAMP</span></span> |<span data-ttu-id="8a3dc-346">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="8a3dc-346">DateTime</span></span> |
| <span data-ttu-id="8a3dc-347">YEREL SAAT DİLİMİ ZAMAN DAMGASI</span><span class="sxs-lookup"><span data-stu-id="8a3dc-347">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="8a3dc-348">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="8a3dc-348">DateTime</span></span> |
| <span data-ttu-id="8a3dc-349">SAAT DİLİMİ ZAMAN DAMGASI</span><span class="sxs-lookup"><span data-stu-id="8a3dc-349">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="8a3dc-350">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="8a3dc-350">DateTime</span></span> |
| <span data-ttu-id="8a3dc-351">İŞARETSİZ TAMSAYI</span><span class="sxs-lookup"><span data-stu-id="8a3dc-351">UNSIGNED INTEGER</span></span> |<span data-ttu-id="8a3dc-352">Sayı</span><span class="sxs-lookup"><span data-stu-id="8a3dc-352">Number</span></span> |
| <span data-ttu-id="8a3dc-353">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="8a3dc-353">VARCHAR2</span></span> |<span data-ttu-id="8a3dc-354">Dize</span><span class="sxs-lookup"><span data-stu-id="8a3dc-354">String</span></span> |
| <span data-ttu-id="8a3dc-355">XML</span><span class="sxs-lookup"><span data-stu-id="8a3dc-355">XML</span></span> |<span data-ttu-id="8a3dc-356">Dize</span><span class="sxs-lookup"><span data-stu-id="8a3dc-356">String</span></span> |

> [!NOTE]
> <span data-ttu-id="8a3dc-357">Veri türü **ARALIĞI yıl Kime ay** ve **ARALIĞI gün için ikinci** Microsoft sürücüsü kullanılırken desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-357">Data type **INTERVAL YEAR TO MONTH** and **INTERVAL DAY TO SECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="8a3dc-358">Kaynak havuzu sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="8a3dc-358">Map source to sink columns</span></span>
<span data-ttu-id="8a3dc-359">Havuz dataset sütunlara kaynak kümesindeki eşleme sütunları hakkında bilgi edinmek için [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="8a3dc-359">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="8a3dc-360">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="8a3dc-360">Repeatable read from relational sources</span></span>
<span data-ttu-id="8a3dc-361">İlişkisel veri kopyalama verileri depoladığında, Yinelenebilirlik istenmeyen sonuçları önlemek için göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-361">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="8a3dc-362">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-362">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="8a3dc-363">Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-363">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="8a3dc-364">Bir dilim iki yolla yeniden çalıştırıldığında, aynı veri dilimi çalıştırmak kaç kez geçtiğinden bağımsız okuduğunuzdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-364">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="8a3dc-365">Bkz: [ilişkisel kaynaktan okumak Repeatable](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="8a3dc-365">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="8a3dc-366">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="8a3dc-366">Performance and Tuning</span></span>
<span data-ttu-id="8a3dc-367">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve onu en iyi duruma getirmek için çeşitli yollar etkisi performansını anahtar Etkenler hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="8a3dc-367">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
