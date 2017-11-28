---
title: Azure Data Factory kullanarak aaaMove verilerden DB2 | Microsoft Docs
description: "Azure Data Factory kopyalama etkinliği kullanarak bir şirket içi DB2 toomove verileri nasıl veritabanı öğrenin"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a><span data-ttu-id="c3b0d-103">Azure Data Factory kopyalama etkinliği kullanarak DB2 taşıma verileri</span><span class="sxs-lookup"><span data-stu-id="c3b0d-103">Move data from DB2 by using Azure Data Factory Copy Activity</span></span>
<span data-ttu-id="c3b0d-104">Bu makalede Azure Data Factory toocopy veri bir şirket içi DB2 veritabanına tooa veri deposundaki kopyalama etkinliği nasıl kullanabileceğinizi açıklar.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-104">This article describes how you can use Copy Activity in Azure Data Factory toocopy data from an on-premises DB2 database tooa data store.</span></span> <span data-ttu-id="c3b0d-105">Merhaba, desteklenen bir havuz olarak listelenen veri tooany deposuna kopyalayabilirsiniz [Data Factory veri taşıma etkinlikleri](data-factory-data-movement-activities.md#supported-data-stores-and-formats) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-105">You can copy data tooany store that is listed as a supported sink in hello [Data Factory data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> <span data-ttu-id="c3b0d-106">Bu konu, kopyalama etkinliği kullanarak veri taşıma genel bir bakış sunar ve desteklenen hello veri deposu birleşimlerini listeler hello Data Factory makale üzerinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-106">This topic builds on hello Data Factory article, which presents an overview of data movement by using Copy Activity and lists hello supported data store combinations.</span></span> 

<span data-ttu-id="c3b0d-107">Veri Fabrikası şu anda bir DB2 veritabanına tooa yalnızca taşıma verilerden destekler [desteklenen havuz veri deposu](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="c3b0d-107">Data Factory currently supports only moving data from a DB2 database tooa [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="c3b0d-108">Verileri diğer veriler taşıma tooa DB2 veritabanına desteklenmiyor depolar.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-108">Moving data from other data stores tooa DB2 database is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3b0d-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c3b0d-109">Prerequisites</span></span>
<span data-ttu-id="c3b0d-110">Veri Fabrikası hello kullanarak bağlanan tooan şirket içi DB2 veritabanına destekler [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="c3b0d-110">Data Factory supports connecting tooan on-premises DB2 database by using hello [data management gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="c3b0d-111">Adım adım yönergeler tooset hello ağ geçidi verileri için verilerinizi toomove kanal bkz hello [şirket içi toocloud veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-111">For step-by-step instructions tooset up hello gateway data pipeline toomove your data, see hello [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="c3b0d-112">Merhaba DB2 Azure Iaas sanal üzerinde barındırılan olsa bile bir ağ geçidi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-112">A gateway is required even if hello DB2 is hosted on Azure IaaS VM.</span></span> <span data-ttu-id="c3b0d-113">Merhaba ağ geçidi üzerinde hello yükleyebilirsiniz hello veri deposu olarak aynı Iaas VM.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-113">You can install hello gateway on hello same IaaS VM as hello data store.</span></span> <span data-ttu-id="c3b0d-114">Hello ağ geçidi toohello veritabanı bağlanırsanız, farklı bir VM hello ağ geçidi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-114">If hello gateway can connect toohello database, you can install hello gateway on a different VM.</span></span>

<span data-ttu-id="c3b0d-115">Yerleşik bir DB2 sürücü Hello veri yönetimi ağ geçidi sağlar, sizin için toomanually sürücü toocopy veri DB2'den yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-115">hello data management gateway provides a built-in DB2 driver, so you don't need toomanually install a driver toocopy data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="c3b0d-116">Merhaba bağlantı ve ağ geçidi sorunları giderme hakkında ipuçları için bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-116">For tips on troubleshooting connection and gateway issues, see hello [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) article.</span></span>


## <a name="supported-versions"></a><span data-ttu-id="c3b0d-117">Desteklenen sürümler</span><span class="sxs-lookup"><span data-stu-id="c3b0d-117">Supported versions</span></span>
<span data-ttu-id="c3b0d-118">Merhaba veri fabrikası DB2 Bağlayıcısı IBM DB2 platformları ve dağıtılmış ilişkisel veritabanı mimarisi (DRDA) SQL Erişim Yöneticisi sürüm 9, 10 ve 11 sürümleriyle aşağıdaki hello destekler:</span><span class="sxs-lookup"><span data-stu-id="c3b0d-118">hello Data Factory DB2 connector supports hello following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager versions 9, 10, and 11:</span></span>

* <span data-ttu-id="c3b0d-119">IBM DB2 z/OS sürümü 11.1 için</span><span class="sxs-lookup"><span data-stu-id="c3b0d-119">IBM DB2 for z/OS version 11.1</span></span>
* <span data-ttu-id="c3b0d-120">IBM DB2 z/OS sürümü 10.1 için</span><span class="sxs-lookup"><span data-stu-id="c3b0d-120">IBM DB2 for z/OS version 10.1</span></span>
* <span data-ttu-id="c3b0d-121">IBM DB2'i (AS400) sürüm 7.2 için</span><span class="sxs-lookup"><span data-stu-id="c3b0d-121">IBM DB2 for i (AS400) version 7.2</span></span>
* <span data-ttu-id="c3b0d-122">IBM DB2'i (AS400) sürüm 7.1 için</span><span class="sxs-lookup"><span data-stu-id="c3b0d-122">IBM DB2 for i (AS400) version 7.1</span></span>
* <span data-ttu-id="c3b0d-123">IBM DB2 Linux, UNIX ve Windows (LUW) sürüm 11</span><span class="sxs-lookup"><span data-stu-id="c3b0d-123">IBM DB2 for Linux, UNIX, and Windows (LUW) version 11</span></span>
* <span data-ttu-id="c3b0d-124">IBM DB2 sürüm 10.5 LUW için</span><span class="sxs-lookup"><span data-stu-id="c3b0d-124">IBM DB2 for LUW version 10.5</span></span>
* <span data-ttu-id="c3b0d-125">IBM DB2 sürüm 10.1 LUW için</span><span class="sxs-lookup"><span data-stu-id="c3b0d-125">IBM DB2 for LUW version 10.1</span></span>

> [!TIP]
> <span data-ttu-id="c3b0d-126">"Hello paket karşılık gelen tooan SQL deyimi yürütme isteği bulunamadı. hello hata iletisi alırsanız</span><span class="sxs-lookup"><span data-stu-id="c3b0d-126">If you receive hello error message "hello package corresponding tooan SQL statement execution request was not found.</span></span> <span data-ttu-id="c3b0d-127">SQLSTATE 51002 SQLCODE =-805, = "hello nedeni hello normal kullanıcı hello işletim sistemi için gerekli bir paketi oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-127">SQLSTATE=51002 SQLCODE=-805," hello reason is a necessary package is not created for hello normal user on hello OS.</span></span> <span data-ttu-id="c3b0d-128">tooresolve Bu sorun, DB2 sunucu türü için aşağıdaki yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="c3b0d-128">tooresolve this issue, follow these instructions for your DB2 server type:</span></span>
> - <span data-ttu-id="c3b0d-129">DB2 için i (AS400): kopyalama etkinliği çalıştırmadan önce hello toplamalarında hello normal kullanıcı oluşturma power user olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-129">DB2 for i (AS400): Let a power user create hello collection for hello normal user before running Copy Activity.</span></span> <span data-ttu-id="c3b0d-130">toocreate hello koleksiyonu, use hello komutu:`create collection <username>`</span><span class="sxs-lookup"><span data-stu-id="c3b0d-130">toocreate hello collection, use hello command: `create collection <username>`</span></span>
> - <span data-ttu-id="c3b0d-131">DB2 için z/OS veya LUW: kullanım yüksek ayrıcalıklı bir hesap--power user veya paket yetkilileri ve bağlama, BINDADD, sahip yönetim toorun hello kez kopya yürütme tooPUBLIC izinleri--verin.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-131">DB2 for z/OS or LUW: Use a high privilege account--a power user or admin that has package authorities and BIND, BINDADD, GRANT EXECUTE tooPUBLIC permissions--toorun hello copy once.</span></span> <span data-ttu-id="c3b0d-132">Merhaba gerekli paketi hello kopyalama sırasında otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-132">hello necessary package is automatically created during hello copy.</span></span> <span data-ttu-id="c3b0d-133">Daha sonra sonraki kopyalama çalışmalarınız için geri toohello normal kullanıcı geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-133">Afterward, you can switch back toohello normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c3b0d-134">Başlarken</span><span class="sxs-lookup"><span data-stu-id="c3b0d-134">Getting started</span></span>
<span data-ttu-id="c3b0d-135">Farklı araçlar ve API'ler kullanarak kopyalama etkinliği toomove verilerle bir şirket içi DB2 veri deposu bir ardışık düzen oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c3b0d-135">You can create a pipeline with a copy activity toomove data from an on-premises DB2 data store by using different tools and APIs:</span></span> 

- <span data-ttu-id="c3b0d-136">Merhaba en kolay yolu toocreate bir ardışık düzen toouse hello Azure Data Factory Kopyalama Sihirbazı ' dir.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-136">hello easiest way toocreate a pipeline is toouse hello Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="c3b0d-137">Hello hızlı bir anlatım hello Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma hakkında bilgi için bkz: [Öğreticisi: hello Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="c3b0d-137">For a quick walkthrough on creating a pipeline by using hello Copy Wizard, see hello [Tutorial: Create a pipeline by using hello Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span> 
- <span data-ttu-id="c3b0d-138">Araçlar toocreate hello Azure portal, Visual Studio, Azure PowerShell, bir Azure Resource Manager şablonu, hello .NET API ve hello gibi bir işlem hattı de kullanabilirsiniz REST API.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-138">You can also use tools toocreate a pipeline, including hello Azure portal, Visual Studio, Azure PowerShell, an Azure Resource Manager template, hello .NET API, and hello REST API.</span></span> <span data-ttu-id="c3b0d-139">Adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için bkz: Merhaba [kopyalama etkinliği Öğreticisi](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="c3b0d-139">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="c3b0d-140">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="c3b0d-140">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="c3b0d-141">Bağlı hizmetler toolink girdi ve çıktı veri depoları tooyour veri fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-141">Create linked services toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="c3b0d-142">Veri kümeleri toorepresent girişi oluşturun ve çıktı verilerini hello kopyalama işlemi için.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-142">Create datasets toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="c3b0d-143">Bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile işlem hattı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-143">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="c3b0d-144">Merhaba, JSON tanımları hello Data Factory bağlı Hizmetleri, kopyalama Sihirbazı'nı kullandığınızda veri kümelerini ve ardışık düzen varlıklar otomatik olarak sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-144">When you use hello Copy Wizard, JSON definitions for hello Data Factory linked services, datasets, and pipeline entities are automatically created for you.</span></span> <span data-ttu-id="c3b0d-145">Araçları veya API'ler (Merhaba dışında .NET API'si) kullandığınızda, hello Data Factory varlıklarını hello JSON biçimi kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-145">When you use tools or APIs (except hello .NET API), you define hello Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="c3b0d-146">Merhaba [JSON örnek: veri DB2 tooAzure Blob Depolama kopyalama](#json-example-copy-data-from-db2-to-azure-blob) hello JSON tanımlarını hello için bir şirket içi DB2 veri deposundaki kullanılan toocopy verileri Data Factory varlıklarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-146">hello [JSON example: Copy data from DB2 tooAzure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) shows hello JSON definitions for hello Data Factory entities that are used toocopy data from an on-premises DB2 data store.</span></span>

<span data-ttu-id="c3b0d-147">Aşağıdaki bölümlerde hello belirli tooa DB2 veri deposudur kullanılan toodefine hello Data Factory varlıklarını JSON özellikleri hello hakkında ayrıntılar verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-147">hello following sections provide details about hello JSON properties that are used toodefine hello Data Factory entities that are specific tooa DB2 data store.</span></span>

## <a name="db2-linked-service-properties"></a><span data-ttu-id="c3b0d-148">DB2 bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="c3b0d-148">DB2 linked service properties</span></span>
<span data-ttu-id="c3b0d-149">Aşağıdaki tablonun hello belirli tooa DB2 bağlantılı hizmet hello JSON özellikleri listeler.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-149">hello following table lists hello JSON properties that are specific tooa DB2 linked service.</span></span>

| <span data-ttu-id="c3b0d-150">Özellik</span><span class="sxs-lookup"><span data-stu-id="c3b0d-150">Property</span></span> | <span data-ttu-id="c3b0d-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c3b0d-151">Description</span></span> | <span data-ttu-id="c3b0d-152">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c3b0d-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3b0d-153">**türü**</span><span class="sxs-lookup"><span data-stu-id="c3b0d-153">**type**</span></span> |<span data-ttu-id="c3b0d-154">Bu özellik çok ayarlanmalıdır**OnPremisesDB2**.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-154">This property must be set too**OnPremisesDB2**.</span></span> |<span data-ttu-id="c3b0d-155">Evet</span><span class="sxs-lookup"><span data-stu-id="c3b0d-155">Yes</span></span> |
| <span data-ttu-id="c3b0d-156">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="c3b0d-156">**server**</span></span> |<span data-ttu-id="c3b0d-157">Merhaba hello DB2 sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-157">hello name of hello DB2 server.</span></span> |<span data-ttu-id="c3b0d-158">Evet</span><span class="sxs-lookup"><span data-stu-id="c3b0d-158">Yes</span></span> |
| <span data-ttu-id="c3b0d-159">**Veritabanı**</span><span class="sxs-lookup"><span data-stu-id="c3b0d-159">**database**</span></span> |<span data-ttu-id="c3b0d-160">Merhaba DB2 veritabanına Hello adı.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-160">hello name of hello DB2 database.</span></span> |<span data-ttu-id="c3b0d-161">Evet</span><span class="sxs-lookup"><span data-stu-id="c3b0d-161">Yes</span></span> |
| <span data-ttu-id="c3b0d-162">**Şema**</span><span class="sxs-lookup"><span data-stu-id="c3b0d-162">**schema**</span></span> |<span data-ttu-id="c3b0d-163">Merhaba şema hello DB2 veritabanında Hello adı.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-163">hello name of hello schema in hello DB2 database.</span></span> <span data-ttu-id="c3b0d-164">Bu özellik, büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-164">This property is case-sensitive.</span></span> |<span data-ttu-id="c3b0d-165">Hayır</span><span class="sxs-lookup"><span data-stu-id="c3b0d-165">No</span></span> |
| <span data-ttu-id="c3b0d-166">**authenticationType**</span><span class="sxs-lookup"><span data-stu-id="c3b0d-166">**authenticationType**</span></span> |<span data-ttu-id="c3b0d-167">kullanılan tooconnect toohello DB2 veritabanı kimlik doğrulaması Hello türü.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-167">hello type of authentication that is used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="c3b0d-168">Merhaba olası değerler şunlardır: Anonim, temel ve Windows.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-168">hello possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="c3b0d-169">Evet</span><span class="sxs-lookup"><span data-stu-id="c3b0d-169">Yes</span></span> |
| <span data-ttu-id="c3b0d-170">**Kullanıcı adı**</span><span class="sxs-lookup"><span data-stu-id="c3b0d-170">**username**</span></span> |<span data-ttu-id="c3b0d-171">Basic veya Windows kimlik doğrulaması kullanırsanız hello kullanıcı hesabı için Hello adı.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-171">hello name for hello user account if you use Basic or Windows authentication.</span></span> |<span data-ttu-id="c3b0d-172">Hayır</span><span class="sxs-lookup"><span data-stu-id="c3b0d-172">No</span></span> |
| <span data-ttu-id="c3b0d-173">**Parola**</span><span class="sxs-lookup"><span data-stu-id="c3b0d-173">**password**</span></span> |<span data-ttu-id="c3b0d-174">Merhaba kullanıcı hesabının parolasını Hello.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-174">hello password for hello user account.</span></span> |<span data-ttu-id="c3b0d-175">Hayır</span><span class="sxs-lookup"><span data-stu-id="c3b0d-175">No</span></span> |
| <span data-ttu-id="c3b0d-176">**gatewayName**</span><span class="sxs-lookup"><span data-stu-id="c3b0d-176">**gatewayName**</span></span> |<span data-ttu-id="c3b0d-177">Data Factory hizmetinin hello hello ağ geçidinin Hello adı tooconnect toohello şirket içi DB2 veritabanına kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-177">hello name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="c3b0d-178">Evet</span><span class="sxs-lookup"><span data-stu-id="c3b0d-178">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="c3b0d-179">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="c3b0d-179">Dataset properties</span></span>
<span data-ttu-id="c3b0d-180">Merhaba hello bölümleri ve veri kümelerini tanımlamak için kullanılabilir özelliklerin listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-180">For a list of hello sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c3b0d-181">Bölümler, gibi **yapısı**, **kullanılabilirlik**ve hello **İlkesi** bir veri kümesi için JSON, tüm veri türleri (Azure SQL, Azure Blob storage, Azure Table için benzer Depolama vb.).</span><span class="sxs-lookup"><span data-stu-id="c3b0d-181">Sections, such as **structure**, **availability**, and hello **policy** for a dataset JSON, are similar for all dataset types (Azure SQL, Azure Blob storage, Azure Table storage, and so on).</span></span>

<span data-ttu-id="c3b0d-182">Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-182">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="c3b0d-183">Merhaba **typeProperties** bir veri kümesi için bir bölüm türü **RelationalTable**, hello DB2 veri kümesini içeren, özellik aşağıdaki hello vardır:</span><span class="sxs-lookup"><span data-stu-id="c3b0d-183">hello **typeProperties** section for a dataset of type **RelationalTable**, which includes hello DB2 dataset, has hello following property:</span></span>

| <span data-ttu-id="c3b0d-184">Özellik</span><span class="sxs-lookup"><span data-stu-id="c3b0d-184">Property</span></span> | <span data-ttu-id="c3b0d-185">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c3b0d-185">Description</span></span> | <span data-ttu-id="c3b0d-186">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c3b0d-186">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3b0d-187">**tableName**</span><span class="sxs-lookup"><span data-stu-id="c3b0d-187">**tableName**</span></span> |<span data-ttu-id="c3b0d-188">Merhaba bağlantılı hizmet hello hello DB2 veritabanı örneğinde Merhaba tablonun adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-188">hello name of hello table in hello DB2 database instance that hello linked service refers to.</span></span> <span data-ttu-id="c3b0d-189">Bu özellik, büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-189">This property is case-sensitive.</span></span> |<span data-ttu-id="c3b0d-190">Hayır (Merhaba, **sorgu** türü kopyalama etkinliği özelliğinin **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="c3b0d-190">No (if hello **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="c3b0d-191">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="c3b0d-191">Copy Activity properties</span></span>
<span data-ttu-id="c3b0d-192">Merhaba hello bölümleri ve kopyalama etkinlikleri tanımlamak için kullanılabilir özelliklerin listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-192">For a list of hello sections and properties that are available for defining copy activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c3b0d-193">Etkinlik özellikleri gibi kopyalamak **adı**, **açıklama**, **girişleri** tablo **çıkarır** tablo ve **İlkesi**, tüm etkinlikler türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-193">Copy Activity properties, such as **name**, **description**, **inputs** table, **outputs** table, and **policy**, are available for all types of activities.</span></span> <span data-ttu-id="c3b0d-194">Merhaba hello kullanılabilir özellikler **typeProperties** her etkinlik türü için hello etkinliğin bölümü.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-194">hello properties that are available in hello **typeProperties** section of hello activity for each activity type.</span></span> <span data-ttu-id="c3b0d-195">Kopya etkinliği için hello özellikleri hello türlerini veri kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-195">For Copy Activity, hello properties vary depending on hello types of data sources and sinks.</span></span>

<span data-ttu-id="c3b0d-196">Kopyalama hello kaynak türü olduğunda etkinliği için **RelationalSource** (içeren DB2), aşağıdaki özelliklere hello hello kullanılabilir **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="c3b0d-196">For Copy Activity, when hello source is of type **RelationalSource** (which includes DB2), hello following properties are available in hello **typeProperties** section:</span></span>

| <span data-ttu-id="c3b0d-197">Özellik</span><span class="sxs-lookup"><span data-stu-id="c3b0d-197">Property</span></span> | <span data-ttu-id="c3b0d-198">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c3b0d-198">Description</span></span> | <span data-ttu-id="c3b0d-199">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="c3b0d-199">Allowed values</span></span> | <span data-ttu-id="c3b0d-200">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c3b0d-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c3b0d-201">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="c3b0d-201">**query**</span></span> |<span data-ttu-id="c3b0d-202">Merhaba özel sorgu tooread hello verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-202">Use hello custom query tooread hello data.</span></span> |<span data-ttu-id="c3b0d-203">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-203">SQL query string.</span></span> <span data-ttu-id="c3b0d-204">Örneğin, `"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="c3b0d-204">For example: `"query": "select * from "MySchema"."MyTable""`</span></span> |<span data-ttu-id="c3b0d-205">Hayır (Merhaba, **tableName** özellik kümesinin belirtilen)</span><span class="sxs-lookup"><span data-stu-id="c3b0d-205">No (if hello **tableName** property of a dataset is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="c3b0d-206">Şema ve tablo adları büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-206">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="c3b0d-207">Merhaba sorgu deyimi içinde özellik adları kullanarak alın "" (çift tırnak).</span><span class="sxs-lookup"><span data-stu-id="c3b0d-207">In hello query statement, enclose property names by using "" (double quotes).</span></span> <span data-ttu-id="c3b0d-208">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c3b0d-208">For example:</span></span>
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a><span data-ttu-id="c3b0d-209">JSON örnek: DB2 tooAzure Blob Depolama veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="c3b0d-209">JSON example: Copy data from DB2 tooAzure Blob storage</span></span>
<span data-ttu-id="c3b0d-210">Bu örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen hello kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c3b0d-210">This example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c3b0d-211">Merhaba örnek nasıl tooBlob depolama toocopy verilerden bir DB2 veritabanına gösterir.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-211">hello example shows you how toocopy data from a DB2 database tooBlob storage.</span></span> <span data-ttu-id="c3b0d-212">Ancak, veriler çok kopyalanabilir[desteklenen herhangi bir veriyi depolamak Havuz türü](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-212">However, data can be copied too[any supported data store sink type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Azure Data Factory Copy Activity.</span></span>

<span data-ttu-id="c3b0d-213">Merhaba örnek Data Factory varlıklarını aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="c3b0d-213">hello sample has hello following Data Factory entities:</span></span>

- <span data-ttu-id="c3b0d-214">Bir DB2 bağlantılı hizmet türü [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="c3b0d-214">A DB2 linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="c3b0d-215">Bir Azure Blob Depolama bağlantılı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="c3b0d-215">An Azure Blob storage linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="c3b0d-216">Bir giriş [dataset](data-factory-create-datasets.md) türü [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="c3b0d-216">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="c3b0d-217">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="c3b0d-217">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="c3b0d-218">A [ardışık düzen](data-factory-create-pipelines.md) hello kullanan kopyalama etkinliği ile [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) özellikleri</span><span class="sxs-lookup"><span data-stu-id="c3b0d-218">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) properties</span></span>

<span data-ttu-id="c3b0d-219">Merhaba örnek veri DB2 veritabanına tooan Azure blob bir sorgu sonucunda saatlik kopyalar.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-219">hello sample copies data from a query result in a DB2 database tooan Azure blob hourly.</span></span> <span data-ttu-id="c3b0d-220">Merhaba örnekte kullanılan JSON özellikleri hello hello varlık tanımları izleyin hello bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-220">hello JSON properties that are used in hello sample are described in hello sections that follow hello entity definitions.</span></span>

<span data-ttu-id="c3b0d-221">İlk adım olarak yükleyin ve bir veri ağ geçidi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-221">As a first step, install and configure a data gateway.</span></span> <span data-ttu-id="c3b0d-222">Yönergelerdir hello [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-222">Instructions are in hello [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="c3b0d-223">**DB2 bağlı hizmet**</span><span class="sxs-lookup"><span data-stu-id="c3b0d-223">**DB2 linked service**</span></span>

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="c3b0d-224">**Azure Blob storage bağlı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="c3b0d-224">**Azure Blob storage linked service**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="c3b0d-225">**DB2 girdi veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="c3b0d-225">**DB2 input dataset**</span></span>

<span data-ttu-id="c3b0d-226">Merhaba örnek DB2 "Merhaba zaman serisi veri için" zaman damgası"etiketli bir sütun sahip MyTable" adlı bir tablo oluşturduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-226">hello sample assumes that you have created a table in DB2 named "MyTable" that has a column labeled "timestamp" for hello time series data.</span></span>

<span data-ttu-id="c3b0d-227">Merhaba **dış** özelliği true olarak ayarlamak çok "."</span><span class="sxs-lookup"><span data-stu-id="c3b0d-227">hello **external** property is set too"true."</span></span> <span data-ttu-id="c3b0d-228">Bu ayar, bu veri kümesi dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil hello Data Factory hizmetinin bildirir.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-228">This setting informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="c3b0d-229">Bu hello fark **türü** özelliği çok ayarlanmış**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-229">Notice that hello **type** property is set too**RelationalTable**.</span></span>


```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

<span data-ttu-id="c3b0d-230">**Azure Blob dataset çıktı**</span><span class="sxs-lookup"><span data-stu-id="c3b0d-230">**Azure Blob output dataset**</span></span>

<span data-ttu-id="c3b0d-231">Veri yazıldığı tooa yeni blob her saat ayarı hello tarafından **sıklığı** özelliği çok "Saat" ve hello **aralığı** özelliği too1.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-231">Data is written tooa new blob every hour by setting hello **frequency** property too"Hour" and hello **interval** property too1.</span></span> <span data-ttu-id="c3b0d-232">Merhaba **folderPath** özelliği hello blob dinamik olarak değerlendirilmesi için işleniyor hello dilimin hello başlangıç zamanı temel alarak.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-232">hello **folderPath** property for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="c3b0d-233">Merhaba klasör yolu hello yıl, ay, gün ve saat bölümlerini hello başlangıç saatini kullanır.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-233">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="c3b0d-234">**Ardışık düzeni için başlangıç kopyalama etkinliği**</span><span class="sxs-lookup"><span data-stu-id="c3b0d-234">**Pipeline for hello copy activity**</span></span>

<span data-ttu-id="c3b0d-235">Merhaba ardışık düzen içeren yapılandırılmış bir kopyalama etkinliği toouse belirtilen giriş ve çıkış veri kümeleri ve saatte zamanlanmış toorun değil.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-235">hello pipeline contains a copy activity that is configured toouse specified input and output datasets and which is scheduled toorun every hour.</span></span> <span data-ttu-id="c3b0d-236">Hello JSON tanımını hello ardışık düzeni için hello **kaynak** türü olarak ayarlanmış çok**RelationalSource** ve hello **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-236">In hello JSON definition for hello pipeline, hello **source** type is set too**RelationalSource** and hello **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="c3b0d-237">Merhaba belirtilen hello SQL sorgusu **sorgu** özelliği hello "Siparişler" tablosundan hello veri seçer.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-237">hello SQL query specified for hello **query** property selects hello data from hello "Orders" table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
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
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a><span data-ttu-id="c3b0d-238">DB2 için tür eşlemesi</span><span class="sxs-lookup"><span data-stu-id="c3b0d-238">Type mapping for DB2</span></span>
<span data-ttu-id="c3b0d-239">Hello belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği, iki aşamalı bir yaklaşım aşağıdaki hello kullanarak kaynak türü toosink türünden otomatik tür dönüşümleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="c3b0d-239">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type toosink type by using hello following two-step approach:</span></span>

1. <span data-ttu-id="c3b0d-240">Yerel kaynak türü tooa .NET türü Dönüştür</span><span class="sxs-lookup"><span data-stu-id="c3b0d-240">Convert from a native source type tooa .NET type</span></span>
2. <span data-ttu-id="c3b0d-241">.NET türü tooa yerel Havuz türü Dönüştür</span><span class="sxs-lookup"><span data-stu-id="c3b0d-241">Convert from a .NET type tooa native sink type</span></span>

<span data-ttu-id="c3b0d-242">Kopya etkinliği bir DB2 türü tooa .NET türünden hello veri dönüştürdüğünde hello aşağıdaki eşlemelerini kullanılır:</span><span class="sxs-lookup"><span data-stu-id="c3b0d-242">hello following mappings are used when Copy Activity converts hello data from a DB2 type tooa .NET type:</span></span>

| <span data-ttu-id="c3b0d-243">DB2 veritabanı türü</span><span class="sxs-lookup"><span data-stu-id="c3b0d-243">DB2 database type</span></span> | <span data-ttu-id="c3b0d-244">.NET framework türü</span><span class="sxs-lookup"><span data-stu-id="c3b0d-244">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="c3b0d-245">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="c3b0d-245">SmallInt</span></span> |<span data-ttu-id="c3b0d-246">Int16</span><span class="sxs-lookup"><span data-stu-id="c3b0d-246">Int16</span></span> |
| <span data-ttu-id="c3b0d-247">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="c3b0d-247">Integer</span></span> |<span data-ttu-id="c3b0d-248">Int32</span><span class="sxs-lookup"><span data-stu-id="c3b0d-248">Int32</span></span> |
| <span data-ttu-id="c3b0d-249">BigInt</span><span class="sxs-lookup"><span data-stu-id="c3b0d-249">BigInt</span></span> |<span data-ttu-id="c3b0d-250">Int64</span><span class="sxs-lookup"><span data-stu-id="c3b0d-250">Int64</span></span> |
| <span data-ttu-id="c3b0d-251">Real</span><span class="sxs-lookup"><span data-stu-id="c3b0d-251">Real</span></span> |<span data-ttu-id="c3b0d-252">Tek</span><span class="sxs-lookup"><span data-stu-id="c3b0d-252">Single</span></span> |
| <span data-ttu-id="c3b0d-253">Çift</span><span class="sxs-lookup"><span data-stu-id="c3b0d-253">Double</span></span> |<span data-ttu-id="c3b0d-254">Çift</span><span class="sxs-lookup"><span data-stu-id="c3b0d-254">Double</span></span> |
| <span data-ttu-id="c3b0d-255">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="c3b0d-255">Float</span></span> |<span data-ttu-id="c3b0d-256">Çift</span><span class="sxs-lookup"><span data-stu-id="c3b0d-256">Double</span></span> |
| <span data-ttu-id="c3b0d-257">Ondalık</span><span class="sxs-lookup"><span data-stu-id="c3b0d-257">Decimal</span></span> |<span data-ttu-id="c3b0d-258">Ondalık</span><span class="sxs-lookup"><span data-stu-id="c3b0d-258">Decimal</span></span> |
| <span data-ttu-id="c3b0d-259">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="c3b0d-259">DecimalFloat</span></span> |<span data-ttu-id="c3b0d-260">Ondalık</span><span class="sxs-lookup"><span data-stu-id="c3b0d-260">Decimal</span></span> |
| <span data-ttu-id="c3b0d-261">sayısal</span><span class="sxs-lookup"><span data-stu-id="c3b0d-261">Numeric</span></span> |<span data-ttu-id="c3b0d-262">Ondalık</span><span class="sxs-lookup"><span data-stu-id="c3b0d-262">Decimal</span></span> |
| <span data-ttu-id="c3b0d-263">Tarih</span><span class="sxs-lookup"><span data-stu-id="c3b0d-263">Date</span></span> |<span data-ttu-id="c3b0d-264">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="c3b0d-264">DateTime</span></span> |
| <span data-ttu-id="c3b0d-265">Zaman</span><span class="sxs-lookup"><span data-stu-id="c3b0d-265">Time</span></span> |<span data-ttu-id="c3b0d-266">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c3b0d-266">TimeSpan</span></span> |
| <span data-ttu-id="c3b0d-267">zaman damgası</span><span class="sxs-lookup"><span data-stu-id="c3b0d-267">Timestamp</span></span> |<span data-ttu-id="c3b0d-268">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="c3b0d-268">DateTime</span></span> |
| <span data-ttu-id="c3b0d-269">XML</span><span class="sxs-lookup"><span data-stu-id="c3b0d-269">Xml</span></span> |<span data-ttu-id="c3b0d-270">Byte]</span><span class="sxs-lookup"><span data-stu-id="c3b0d-270">Byte[]</span></span> |
| <span data-ttu-id="c3b0d-271">char</span><span class="sxs-lookup"><span data-stu-id="c3b0d-271">Char</span></span> |<span data-ttu-id="c3b0d-272">Dize</span><span class="sxs-lookup"><span data-stu-id="c3b0d-272">String</span></span> |
| <span data-ttu-id="c3b0d-273">VarChar</span><span class="sxs-lookup"><span data-stu-id="c3b0d-273">VarChar</span></span> |<span data-ttu-id="c3b0d-274">Dize</span><span class="sxs-lookup"><span data-stu-id="c3b0d-274">String</span></span> |
| <span data-ttu-id="c3b0d-275">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="c3b0d-275">LongVarChar</span></span> |<span data-ttu-id="c3b0d-276">Dize</span><span class="sxs-lookup"><span data-stu-id="c3b0d-276">String</span></span> |
| <span data-ttu-id="c3b0d-277">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="c3b0d-277">DB2DynArray</span></span> |<span data-ttu-id="c3b0d-278">Dize</span><span class="sxs-lookup"><span data-stu-id="c3b0d-278">String</span></span> |
| <span data-ttu-id="c3b0d-279">İkili</span><span class="sxs-lookup"><span data-stu-id="c3b0d-279">Binary</span></span> |<span data-ttu-id="c3b0d-280">Byte]</span><span class="sxs-lookup"><span data-stu-id="c3b0d-280">Byte[]</span></span> |
| <span data-ttu-id="c3b0d-281">VarBinary</span><span class="sxs-lookup"><span data-stu-id="c3b0d-281">VarBinary</span></span> |<span data-ttu-id="c3b0d-282">Byte]</span><span class="sxs-lookup"><span data-stu-id="c3b0d-282">Byte[]</span></span> |
| <span data-ttu-id="c3b0d-283">LONGVARBINARY</span><span class="sxs-lookup"><span data-stu-id="c3b0d-283">LongVarBinary</span></span> |<span data-ttu-id="c3b0d-284">Byte]</span><span class="sxs-lookup"><span data-stu-id="c3b0d-284">Byte[]</span></span> |
| <span data-ttu-id="c3b0d-285">Grafiği</span><span class="sxs-lookup"><span data-stu-id="c3b0d-285">Graphic</span></span> |<span data-ttu-id="c3b0d-286">Dize</span><span class="sxs-lookup"><span data-stu-id="c3b0d-286">String</span></span> |
| <span data-ttu-id="c3b0d-287">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="c3b0d-287">VarGraphic</span></span> |<span data-ttu-id="c3b0d-288">Dize</span><span class="sxs-lookup"><span data-stu-id="c3b0d-288">String</span></span> |
| <span data-ttu-id="c3b0d-289">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="c3b0d-289">LongVarGraphic</span></span> |<span data-ttu-id="c3b0d-290">Dize</span><span class="sxs-lookup"><span data-stu-id="c3b0d-290">String</span></span> |
| <span data-ttu-id="c3b0d-291">CLOB</span><span class="sxs-lookup"><span data-stu-id="c3b0d-291">Clob</span></span> |<span data-ttu-id="c3b0d-292">Dize</span><span class="sxs-lookup"><span data-stu-id="c3b0d-292">String</span></span> |
| <span data-ttu-id="c3b0d-293">Blob</span><span class="sxs-lookup"><span data-stu-id="c3b0d-293">Blob</span></span> |<span data-ttu-id="c3b0d-294">Byte]</span><span class="sxs-lookup"><span data-stu-id="c3b0d-294">Byte[]</span></span> |
| <span data-ttu-id="c3b0d-295">DbClob</span><span class="sxs-lookup"><span data-stu-id="c3b0d-295">DbClob</span></span> |<span data-ttu-id="c3b0d-296">Dize</span><span class="sxs-lookup"><span data-stu-id="c3b0d-296">String</span></span> |
| <span data-ttu-id="c3b0d-297">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="c3b0d-297">SmallInt</span></span> |<span data-ttu-id="c3b0d-298">Int16</span><span class="sxs-lookup"><span data-stu-id="c3b0d-298">Int16</span></span> |
| <span data-ttu-id="c3b0d-299">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="c3b0d-299">Integer</span></span> |<span data-ttu-id="c3b0d-300">Int32</span><span class="sxs-lookup"><span data-stu-id="c3b0d-300">Int32</span></span> |
| <span data-ttu-id="c3b0d-301">BigInt</span><span class="sxs-lookup"><span data-stu-id="c3b0d-301">BigInt</span></span> |<span data-ttu-id="c3b0d-302">Int64</span><span class="sxs-lookup"><span data-stu-id="c3b0d-302">Int64</span></span> |
| <span data-ttu-id="c3b0d-303">Real</span><span class="sxs-lookup"><span data-stu-id="c3b0d-303">Real</span></span> |<span data-ttu-id="c3b0d-304">Tek</span><span class="sxs-lookup"><span data-stu-id="c3b0d-304">Single</span></span> |
| <span data-ttu-id="c3b0d-305">Çift</span><span class="sxs-lookup"><span data-stu-id="c3b0d-305">Double</span></span> |<span data-ttu-id="c3b0d-306">Çift</span><span class="sxs-lookup"><span data-stu-id="c3b0d-306">Double</span></span> |
| <span data-ttu-id="c3b0d-307">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="c3b0d-307">Float</span></span> |<span data-ttu-id="c3b0d-308">Çift</span><span class="sxs-lookup"><span data-stu-id="c3b0d-308">Double</span></span> |
| <span data-ttu-id="c3b0d-309">Ondalık</span><span class="sxs-lookup"><span data-stu-id="c3b0d-309">Decimal</span></span> |<span data-ttu-id="c3b0d-310">Ondalık</span><span class="sxs-lookup"><span data-stu-id="c3b0d-310">Decimal</span></span> |
| <span data-ttu-id="c3b0d-311">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="c3b0d-311">DecimalFloat</span></span> |<span data-ttu-id="c3b0d-312">Ondalık</span><span class="sxs-lookup"><span data-stu-id="c3b0d-312">Decimal</span></span> |
| <span data-ttu-id="c3b0d-313">sayısal</span><span class="sxs-lookup"><span data-stu-id="c3b0d-313">Numeric</span></span> |<span data-ttu-id="c3b0d-314">Ondalık</span><span class="sxs-lookup"><span data-stu-id="c3b0d-314">Decimal</span></span> |
| <span data-ttu-id="c3b0d-315">Tarih</span><span class="sxs-lookup"><span data-stu-id="c3b0d-315">Date</span></span> |<span data-ttu-id="c3b0d-316">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="c3b0d-316">DateTime</span></span> |
| <span data-ttu-id="c3b0d-317">Zaman</span><span class="sxs-lookup"><span data-stu-id="c3b0d-317">Time</span></span> |<span data-ttu-id="c3b0d-318">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c3b0d-318">TimeSpan</span></span> |
| <span data-ttu-id="c3b0d-319">zaman damgası</span><span class="sxs-lookup"><span data-stu-id="c3b0d-319">Timestamp</span></span> |<span data-ttu-id="c3b0d-320">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="c3b0d-320">DateTime</span></span> |
| <span data-ttu-id="c3b0d-321">XML</span><span class="sxs-lookup"><span data-stu-id="c3b0d-321">Xml</span></span> |<span data-ttu-id="c3b0d-322">Byte]</span><span class="sxs-lookup"><span data-stu-id="c3b0d-322">Byte[]</span></span> |
| <span data-ttu-id="c3b0d-323">char</span><span class="sxs-lookup"><span data-stu-id="c3b0d-323">Char</span></span> |<span data-ttu-id="c3b0d-324">Dize</span><span class="sxs-lookup"><span data-stu-id="c3b0d-324">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="c3b0d-325">Kaynak toosink sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="c3b0d-325">Map source toosink columns</span></span>
<span data-ttu-id="c3b0d-326">hello kaynak dataset toocolumns hello havuz kümesindeki toomap sütunlarında nasıl görürüm toolearn [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c3b0d-326">toolearn how toomap columns in hello source dataset toocolumns in hello sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="c3b0d-327">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="c3b0d-327">Repeatable reads from relational sources</span></span>
<span data-ttu-id="c3b0d-328">İlişkisel veri deposundan verileri kopyaladığınızda, Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-328">When you copy data from a relational data store, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="c3b0d-329">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-329">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="c3b0d-330">Merhaba yeniden deneme de yapılandırabilirsiniz **İlkesi** özelliği için bir veri kümesi toorerun bir hata oluştuğunda bir dilim.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-330">You can also configure hello retry **policy** property for a dataset toorerun a slice when a failure occurs.</span></span> <span data-ttu-id="c3b0d-331">Merhaba aynı veri nasıl geçtiğinden bağımsız okuma emin olun birçok kez hello dilimi yeniden çalıştırın ve ne olursa olsun, nasıl hello dilimi yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c3b0d-331">Make sure that hello same data is read no matter how many times hello slice is rerun, and regardless of how you rerun hello slice.</span></span> <span data-ttu-id="c3b0d-332">Daha fazla bilgi için bkz: [Repeatable okur ilişkisel kaynaklardan](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="c3b0d-332">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c3b0d-333">Performans ve ayar</span><span class="sxs-lookup"><span data-stu-id="c3b0d-333">Performance and tuning</span></span>
<span data-ttu-id="c3b0d-334">Kopyalama etkinliği ve yolları toooptimize performans hello hello performansını etkileyen anahtar Etkenler hakkında bilgi edinin [kopya etkinliği performansının ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="c3b0d-334">Learn about key factors that affect hello performance of Copy Activity and ways toooptimize performance in hello [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
