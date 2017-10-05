---
title: "Azure Data Factory kullanarak DB2'den veri taşıma | Microsoft Docs"
description: "Azure Data Factory kopyalama etkinliği kullanarak bir şirket içi DB2 veritabanından veri taşıma hakkında bilgi edinin"
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
ms.openlocfilehash: 6a89cc44724dbb5b46a9e89d6da24d9b35ddbbef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a><span data-ttu-id="9d0fa-103">Azure Data Factory kopyalama etkinliği kullanarak DB2 taşıma verileri</span><span class="sxs-lookup"><span data-stu-id="9d0fa-103">Move data from DB2 by using Azure Data Factory Copy Activity</span></span>
<span data-ttu-id="9d0fa-104">Bu makalede kopya etkinliği Azure Data Factory'de veri bir şirket içi DB2 veritabanından veri deposuna kopyalamak için nasıl kullanabileceğinizi açıklar.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-104">This article describes how you can use Copy Activity in Azure Data Factory to copy data from an on-premises DB2 database to a data store.</span></span> <span data-ttu-id="9d0fa-105">Desteklenen bir havuz olarak listelenen tüm depolama, veri kopyalayabilirsiniz [Data Factory veri taşıma etkinlikleri](data-factory-data-movement-activities.md#supported-data-stores-and-formats) makalesi.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-105">You can copy data to any store that is listed as a supported sink in the [Data Factory data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> <span data-ttu-id="9d0fa-106">Bu konu, kopyalama etkinliği kullanarak veri taşıma genel bir bakış sunar ve desteklenen veri deposu birleşimlerini listeler Data Factory makale oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-106">This topic builds on the Data Factory article, which presents an overview of data movement by using Copy Activity and lists the supported data store combinations.</span></span> 

<span data-ttu-id="9d0fa-107">Veri Fabrikası şu anda bir DB2 veritabanından yalnızca veri taşımayı destekleyen bir [desteklenen havuz veri deposu](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="9d0fa-107">Data Factory currently supports only moving data from a DB2 database to a [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="9d0fa-108">Verileri diğer veriler taşıma veritabanı desteklenmiyor bir DB2 depolar.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-108">Moving data from other data stores to a DB2 database is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d0fa-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9d0fa-109">Prerequisites</span></span>
<span data-ttu-id="9d0fa-110">Veri Fabrikası destekleyen kullanarak bir şirket içi DB2 veritabanına bağlanma [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="9d0fa-110">Data Factory supports connecting to an on-premises DB2 database by using the [data management gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="9d0fa-111">Verilerinizi taşımak için ağ geçidi veri ardışık ayarlamak adım adım yönergeler için bkz: [buluta şirket içinden veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-111">For step-by-step instructions to set up the gateway data pipeline to move your data, see the [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="9d0fa-112">DB2 Azure Iaas sanal üzerinde barındırılıyorsa bile bir ağ geçidi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-112">A gateway is required even if the DB2 is hosted on Azure IaaS VM.</span></span> <span data-ttu-id="9d0fa-113">Veri deposu olarak aynı Iaas VM ağ geçidi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-113">You can install the gateway on the same IaaS VM as the data store.</span></span> <span data-ttu-id="9d0fa-114">Ağ geçidi veritabanına bağlanıyorsanız, farklı bir sanal ağ geçidi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-114">If the gateway can connect to the database, you can install the gateway on a different VM.</span></span>

<span data-ttu-id="9d0fa-115">Veri Yönetimi ağ geçidi yerleşik bir DB2 sürücü sağlar, DB2'den verileri kopyalamak için bir sürücüyü el ile yüklemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-115">The data management gateway provides a built-in DB2 driver, so you don't need to manually install a driver to copy data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="9d0fa-116">Bağlantı ve ağ geçidi sorunları giderme hakkında ipuçları için bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) makalesi.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-116">For tips on troubleshooting connection and gateway issues, see the [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) article.</span></span>


## <a name="supported-versions"></a><span data-ttu-id="9d0fa-117">Desteklenen sürümler</span><span class="sxs-lookup"><span data-stu-id="9d0fa-117">Supported versions</span></span>
<span data-ttu-id="9d0fa-118">Veri Fabrikası DB2 Bağlayıcısı'nı aşağıdaki IBM DB2 platformları ve dağıtılmış ilişkisel veritabanı mimarisi (DRDA) SQL Erişim Yöneticisi sürüm 9, 10 ve 11 sürümleriyle destekler:</span><span class="sxs-lookup"><span data-stu-id="9d0fa-118">The Data Factory DB2 connector supports the following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager versions 9, 10, and 11:</span></span>

* <span data-ttu-id="9d0fa-119">IBM DB2 z/OS sürümü 11.1 için</span><span class="sxs-lookup"><span data-stu-id="9d0fa-119">IBM DB2 for z/OS version 11.1</span></span>
* <span data-ttu-id="9d0fa-120">IBM DB2 z/OS sürümü 10.1 için</span><span class="sxs-lookup"><span data-stu-id="9d0fa-120">IBM DB2 for z/OS version 10.1</span></span>
* <span data-ttu-id="9d0fa-121">IBM DB2'i (AS400) sürüm 7.2 için</span><span class="sxs-lookup"><span data-stu-id="9d0fa-121">IBM DB2 for i (AS400) version 7.2</span></span>
* <span data-ttu-id="9d0fa-122">IBM DB2'i (AS400) sürüm 7.1 için</span><span class="sxs-lookup"><span data-stu-id="9d0fa-122">IBM DB2 for i (AS400) version 7.1</span></span>
* <span data-ttu-id="9d0fa-123">IBM DB2 Linux, UNIX ve Windows (LUW) sürüm 11</span><span class="sxs-lookup"><span data-stu-id="9d0fa-123">IBM DB2 for Linux, UNIX, and Windows (LUW) version 11</span></span>
* <span data-ttu-id="9d0fa-124">IBM DB2 sürüm 10.5 LUW için</span><span class="sxs-lookup"><span data-stu-id="9d0fa-124">IBM DB2 for LUW version 10.5</span></span>
* <span data-ttu-id="9d0fa-125">IBM DB2 sürüm 10.1 LUW için</span><span class="sxs-lookup"><span data-stu-id="9d0fa-125">IBM DB2 for LUW version 10.1</span></span>

> [!TIP]
> <span data-ttu-id="9d0fa-126">"Bir SQL deyimi yürütme isteğine karşılık gelen paket bulunamadı. hata iletisi alırsanız</span><span class="sxs-lookup"><span data-stu-id="9d0fa-126">If you receive the error message "The package corresponding to an SQL statement execution request was not found.</span></span> <span data-ttu-id="9d0fa-127">SQLSTATE 51002 SQLCODE =-805, = "işletim sistemi normal kullanıcı için gerekli bir paketi oluşturulmaz nedenidir.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-127">SQLSTATE=51002 SQLCODE=-805," the reason is a necessary package is not created for the normal user on the OS.</span></span> <span data-ttu-id="9d0fa-128">Bu sorunu çözmek için DB2 sunucu türü için bu yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="9d0fa-128">To resolve this issue, follow these instructions for your DB2 server type:</span></span>
> - <span data-ttu-id="9d0fa-129">DB2 için i (AS400): kopyalama etkinliği çalıştırmadan önce normal bir kullanıcı için koleksiyonu oluşturun power user olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-129">DB2 for i (AS400): Let a power user create the collection for the normal user before running Copy Activity.</span></span> <span data-ttu-id="9d0fa-130">Koleksiyonu oluşturmak için komutu kullanın:`create collection <username>`</span><span class="sxs-lookup"><span data-stu-id="9d0fa-130">To create the collection, use the command: `create collection <username>`</span></span>
> - <span data-ttu-id="9d0fa-131">DB2 için z/OS veya LUW: ortak izin kopya kez çalıştırmak için--verme yürütme yüksek ayrıcalıklı bir hesap--power user veya paket yetkilileri ve bağlama, BINDADD, sahip yönetim kullanın.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-131">DB2 for z/OS or LUW: Use a high privilege account--a power user or admin that has package authorities and BIND, BINDADD, GRANT EXECUTE TO PUBLIC permissions--to run the copy once.</span></span> <span data-ttu-id="9d0fa-132">Gerekli paketi kopyalama sırasında otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-132">The necessary package is automatically created during the copy.</span></span> <span data-ttu-id="9d0fa-133">Daha sonra sonraki kopyalama çalışmalarınız için normal kullanıcının geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-133">Afterward, you can switch back to the normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="9d0fa-134">Başlarken</span><span class="sxs-lookup"><span data-stu-id="9d0fa-134">Getting started</span></span>
<span data-ttu-id="9d0fa-135">Farklı araçlar ve API'ler kullanarak bir şirket içi DB2 veri deposundan verileri taşımak için kopyalama etkinliği ile işlem hattı oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9d0fa-135">You can create a pipeline with a copy activity to move data from an on-premises DB2 data store by using different tools and APIs:</span></span> 

- <span data-ttu-id="9d0fa-136">Bir işlem hattı oluşturmak için en kolay yolu, Azure Data Factory Kopyalama Sihirbazı'nı kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-136">The easiest way to create a pipeline is to use the Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="9d0fa-137">Hızlı bir anlatım Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma hakkında bilgi için bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="9d0fa-137">For a quick walkthrough on creating a pipeline by using the Copy Wizard, see the [Tutorial: Create a pipeline by using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span> 
- <span data-ttu-id="9d0fa-138">Azure portalı, Visual Studio, Azure PowerShell, Azure Resource Manager şablonu, .NET API ve REST API de dahil olmak üzere bir işlem hattı oluşturmak için araçlar da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-138">You can also use tools to create a pipeline, including the Azure portal, Visual Studio, Azure PowerShell, an Azure Resource Manager template, the .NET API, and the REST API.</span></span> <span data-ttu-id="9d0fa-139">Kopyalama etkinliği ile işlem hattı oluşturmak adım adım yönergeler için bkz: [kopyalama etkinliği Öğreticisi](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="9d0fa-139">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="9d0fa-140">Araçlar ya da API'leri kullanıp bir havuz veri deposu için bir kaynak veri deposundan verileri taşır bir ardışık düzen oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="9d0fa-140">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="9d0fa-141">Veri depoları, veri fabrikası için çıkış ve giriş bağlantısı bağlantılı Hizmetleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-141">Create linked services to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="9d0fa-142">Kopyalama işlemi için girdi ve çıktı verilerini temsil edecek veri kümeleri oluşturma.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-142">Create datasets to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="9d0fa-143">Bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile işlem hattı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-143">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="9d0fa-144">Data Factory bağlantılı için JSON tanımları, kopyalama Sihirbazı'nı kullandığınızda, hizmetler, veri kümelerini ve ardışık düzen varlıklar otomatik olarak sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-144">When you use the Copy Wizard, JSON definitions for the Data Factory linked services, datasets, and pipeline entities are automatically created for you.</span></span> <span data-ttu-id="9d0fa-145">Araçları veya API'ler (dışında .NET API'si) kullandığınızda, JSON biçimini kullanarak Data Factory varlıklarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-145">When you use tools or APIs (except the .NET API), you define the Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="9d0fa-146">[JSON örnek: veri kopyalama DB2'den Azure Blob depolama alanına](#json-example-copy-data-from-db2-to-azure-blob) bir şirket içi DB2 veri deposundan verileri kopyalamak için kullanılan Data Factory varlıkları için JSON tanımları gösterir.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-146">The [JSON example: Copy data from DB2 to Azure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) shows the JSON definitions for the Data Factory entities that are used to copy data from an on-premises DB2 data store.</span></span>

<span data-ttu-id="9d0fa-147">Aşağıdaki bölümler, belirli bir DB2 veri deposuna Data Factory varlıklarını tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-147">The following sections provide details about the JSON properties that are used to define the Data Factory entities that are specific to a DB2 data store.</span></span>

## <a name="db2-linked-service-properties"></a><span data-ttu-id="9d0fa-148">DB2 bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="9d0fa-148">DB2 linked service properties</span></span>
<span data-ttu-id="9d0fa-149">Aşağıdaki tabloda bir DB2 bağlantılı hizmete özel JSON özellikleri listeler.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-149">The following table lists the JSON properties that are specific to a DB2 linked service.</span></span>

| <span data-ttu-id="9d0fa-150">Özellik</span><span class="sxs-lookup"><span data-stu-id="9d0fa-150">Property</span></span> | <span data-ttu-id="9d0fa-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9d0fa-151">Description</span></span> | <span data-ttu-id="9d0fa-152">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9d0fa-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9d0fa-153">**türü**</span><span class="sxs-lookup"><span data-stu-id="9d0fa-153">**type**</span></span> |<span data-ttu-id="9d0fa-154">Bu özelliği ayarlamak **OnPremisesDB2**.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-154">This property must be set to **OnPremisesDB2**.</span></span> |<span data-ttu-id="9d0fa-155">Evet</span><span class="sxs-lookup"><span data-stu-id="9d0fa-155">Yes</span></span> |
| <span data-ttu-id="9d0fa-156">**Sunucu**</span><span class="sxs-lookup"><span data-stu-id="9d0fa-156">**server**</span></span> |<span data-ttu-id="9d0fa-157">DB2 sunucunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-157">The name of the DB2 server.</span></span> |<span data-ttu-id="9d0fa-158">Evet</span><span class="sxs-lookup"><span data-stu-id="9d0fa-158">Yes</span></span> |
| <span data-ttu-id="9d0fa-159">**Veritabanı**</span><span class="sxs-lookup"><span data-stu-id="9d0fa-159">**database**</span></span> |<span data-ttu-id="9d0fa-160">DB2 veritabanının adı.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-160">The name of the DB2 database.</span></span> |<span data-ttu-id="9d0fa-161">Evet</span><span class="sxs-lookup"><span data-stu-id="9d0fa-161">Yes</span></span> |
| <span data-ttu-id="9d0fa-162">**Şema**</span><span class="sxs-lookup"><span data-stu-id="9d0fa-162">**schema**</span></span> |<span data-ttu-id="9d0fa-163">DB2 veritabanında şema adı.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-163">The name of the schema in the DB2 database.</span></span> <span data-ttu-id="9d0fa-164">Bu özellik, büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-164">This property is case-sensitive.</span></span> |<span data-ttu-id="9d0fa-165">Hayır</span><span class="sxs-lookup"><span data-stu-id="9d0fa-165">No</span></span> |
| <span data-ttu-id="9d0fa-166">**authenticationType**</span><span class="sxs-lookup"><span data-stu-id="9d0fa-166">**authenticationType**</span></span> |<span data-ttu-id="9d0fa-167">DB2 veritabanına bağlanmak için kullanılan kimlik doğrulama türü.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-167">The type of authentication that is used to connect to the DB2 database.</span></span> <span data-ttu-id="9d0fa-168">Olası değerler şunlardır: Anonim, temel ve Windows.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-168">The possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="9d0fa-169">Evet</span><span class="sxs-lookup"><span data-stu-id="9d0fa-169">Yes</span></span> |
| <span data-ttu-id="9d0fa-170">**Kullanıcı adı**</span><span class="sxs-lookup"><span data-stu-id="9d0fa-170">**username**</span></span> |<span data-ttu-id="9d0fa-171">Basic veya Windows kimlik doğrulaması kullanıyorsanız, kullanıcı hesabının adı.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-171">The name for the user account if you use Basic or Windows authentication.</span></span> |<span data-ttu-id="9d0fa-172">Hayır</span><span class="sxs-lookup"><span data-stu-id="9d0fa-172">No</span></span> |
| <span data-ttu-id="9d0fa-173">**Parola**</span><span class="sxs-lookup"><span data-stu-id="9d0fa-173">**password**</span></span> |<span data-ttu-id="9d0fa-174">Kullanıcı hesabının parolası.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-174">The password for the user account.</span></span> |<span data-ttu-id="9d0fa-175">Hayır</span><span class="sxs-lookup"><span data-stu-id="9d0fa-175">No</span></span> |
| <span data-ttu-id="9d0fa-176">**gatewayName**</span><span class="sxs-lookup"><span data-stu-id="9d0fa-176">**gatewayName**</span></span> |<span data-ttu-id="9d0fa-177">Data Factory hizmetinin şirket içi DB2 veritabanına bağlanmak için kullanması gereken ağ geçidinin adı.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-177">The name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="9d0fa-178">Evet</span><span class="sxs-lookup"><span data-stu-id="9d0fa-178">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="9d0fa-179">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="9d0fa-179">Dataset properties</span></span>
<span data-ttu-id="9d0fa-180">Bölümleri ve veri kümelerini tanımlamak için kullanılabilir özelliklerin listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-180">For a list of the sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="9d0fa-181">Bölümler, gibi **yapısı**, **kullanılabilirlik**ve **İlkesi** bir veri kümesi için JSON, tüm veri kümesi türleri (Azure SQL, Azure Blob Depolama, Azure Table depolama için benzer vb.).</span><span class="sxs-lookup"><span data-stu-id="9d0fa-181">Sections, such as **structure**, **availability**, and the **policy** for a dataset JSON, are similar for all dataset types (Azure SQL, Azure Blob storage, Azure Table storage, and so on).</span></span>

<span data-ttu-id="9d0fa-182">**TypeProperties** bölüm veri kümesi her tür için farklıdır ve verilerin veri deposunda konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-182">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="9d0fa-183">**TypeProperties** bir veri kümesi için bir bölüm türü **RelationalTable**, DB2 veri kümesini içeren aşağıdaki özelliğe sahiptir:</span><span class="sxs-lookup"><span data-stu-id="9d0fa-183">The **typeProperties** section for a dataset of type **RelationalTable**, which includes the DB2 dataset, has the following property:</span></span>

| <span data-ttu-id="9d0fa-184">Özellik</span><span class="sxs-lookup"><span data-stu-id="9d0fa-184">Property</span></span> | <span data-ttu-id="9d0fa-185">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9d0fa-185">Description</span></span> | <span data-ttu-id="9d0fa-186">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9d0fa-186">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9d0fa-187">**tableName**</span><span class="sxs-lookup"><span data-stu-id="9d0fa-187">**tableName**</span></span> |<span data-ttu-id="9d0fa-188">DB2 veritabanı örneğinde bağlantılı hizmet başvurduğu tablonun adı.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-188">The name of the table in the DB2 database instance that the linked service refers to.</span></span> <span data-ttu-id="9d0fa-189">Bu özellik, büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-189">This property is case-sensitive.</span></span> |<span data-ttu-id="9d0fa-190">Hayır (varsa **sorgu** türü kopyalama etkinliği özelliğinin **RelationalSource** belirtilir)</span><span class="sxs-lookup"><span data-stu-id="9d0fa-190">No (if the **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="9d0fa-191">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="9d0fa-191">Copy Activity properties</span></span>
<span data-ttu-id="9d0fa-192">Bölümleri ve kopyalama etkinlikleri tanımlamak için kullanılabilir olan özelliklerin listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-192">For a list of the sections and properties that are available for defining copy activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="9d0fa-193">Etkinlik özellikleri gibi kopyalamak **adı**, **açıklama**, **girişleri** tablo **çıkarır** tablo ve **İlkesi**, tüm etkinlikler türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-193">Copy Activity properties, such as **name**, **description**, **inputs** table, **outputs** table, and **policy**, are available for all types of activities.</span></span> <span data-ttu-id="9d0fa-194">Kullanılabilir özellikler **typeProperties** her etkinlik türü için etkinliğin bölümü.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-194">The properties that are available in the **typeProperties** section of the activity for each activity type.</span></span> <span data-ttu-id="9d0fa-195">Kopya etkinliği için özellikleri, veri kaynaklarının ve havuzlarını türlerine bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-195">For Copy Activity, the properties vary depending on the types of data sources and sinks.</span></span>

<span data-ttu-id="9d0fa-196">Kopyalama kaynağı türü olduğunda etkinliği için **RelationalSource** (içeren DB2), aşağıdaki özellikler mevcuttur **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="9d0fa-196">For Copy Activity, when the source is of type **RelationalSource** (which includes DB2), the following properties are available in the **typeProperties** section:</span></span>

| <span data-ttu-id="9d0fa-197">Özellik</span><span class="sxs-lookup"><span data-stu-id="9d0fa-197">Property</span></span> | <span data-ttu-id="9d0fa-198">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9d0fa-198">Description</span></span> | <span data-ttu-id="9d0fa-199">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="9d0fa-199">Allowed values</span></span> | <span data-ttu-id="9d0fa-200">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9d0fa-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9d0fa-201">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="9d0fa-201">**query**</span></span> |<span data-ttu-id="9d0fa-202">Verileri okumak için özel sorgu kullanın.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-202">Use the custom query to read the data.</span></span> |<span data-ttu-id="9d0fa-203">SQL sorgu dizesi.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-203">SQL query string.</span></span> <span data-ttu-id="9d0fa-204">Örneğin, `"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="9d0fa-204">For example: `"query": "select * from "MySchema"."MyTable""`</span></span> |<span data-ttu-id="9d0fa-205">Hayır (varsa **tableName** özellik kümesinin belirtilen)</span><span class="sxs-lookup"><span data-stu-id="9d0fa-205">No (if the **tableName** property of a dataset is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="9d0fa-206">Şema ve tablo adları büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-206">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="9d0fa-207">Sorgu deyimini kullanarak özellik adları alın "" (çift tırnak).</span><span class="sxs-lookup"><span data-stu-id="9d0fa-207">In the query statement, enclose property names by using "" (double quotes).</span></span> <span data-ttu-id="9d0fa-208">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="9d0fa-208">For example:</span></span>
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-to-azure-blob-storage"></a><span data-ttu-id="9d0fa-209">JSON örnek: veri kopyalama DB2'den Azure Blob depolama alanına</span><span class="sxs-lookup"><span data-stu-id="9d0fa-209">JSON example: Copy data from DB2 to Azure Blob storage</span></span>
<span data-ttu-id="9d0fa-210">Bu örnek kullanarak bir işlem hattı oluşturmak için kullanabileceğiniz örnek JSON tanımları sağlar, [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9d0fa-210">This example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="9d0fa-211">Örnek veri DB2 veritabanından Blob depolama alanına kopyalama gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-211">The example shows you how to copy data from a DB2 database to Blob storage.</span></span> <span data-ttu-id="9d0fa-212">Ancak, veriler için kopyalanabilir [desteklenen herhangi bir veriyi depolamak Havuz türü](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-212">However, data can be copied to [any supported data store sink type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Azure Data Factory Copy Activity.</span></span>

<span data-ttu-id="9d0fa-213">Örnek aşağıdaki Data Factory varlıklarını sahiptir:</span><span class="sxs-lookup"><span data-stu-id="9d0fa-213">The sample has the following Data Factory entities:</span></span>

- <span data-ttu-id="9d0fa-214">Bir DB2 bağlantılı hizmet türü [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="9d0fa-214">A DB2 linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="9d0fa-215">Bir Azure Blob Depolama bağlantılı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="9d0fa-215">An Azure Blob storage linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="9d0fa-216">Bir giriş [dataset](data-factory-create-datasets.md) türü [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="9d0fa-216">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="9d0fa-217">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="9d0fa-217">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="9d0fa-218">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) özellikleri</span><span class="sxs-lookup"><span data-stu-id="9d0fa-218">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses the [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) properties</span></span>

<span data-ttu-id="9d0fa-219">Örnek veri DB2 veritabanına bir sorgu sonucunda bir Azure blob saatlik kopyalar.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-219">The sample copies data from a query result in a DB2 database to an Azure blob hourly.</span></span> <span data-ttu-id="9d0fa-220">Aşağıdaki örnekte kullanılan JSON özellikleri varlık tanımları izleyen bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-220">The JSON properties that are used in the sample are described in the sections that follow the entity definitions.</span></span>

<span data-ttu-id="9d0fa-221">İlk adım olarak yükleyin ve bir veri ağ geçidi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-221">As a first step, install and configure a data gateway.</span></span> <span data-ttu-id="9d0fa-222">Yönergeler [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-222">Instructions are in the [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="9d0fa-223">**DB2 bağlı hizmet**</span><span class="sxs-lookup"><span data-stu-id="9d0fa-223">**DB2 linked service**</span></span>

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

<span data-ttu-id="9d0fa-224">**Azure Blob storage bağlı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="9d0fa-224">**Azure Blob storage linked service**</span></span>

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

<span data-ttu-id="9d0fa-225">**DB2 girdi veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="9d0fa-225">**DB2 input dataset**</span></span>

<span data-ttu-id="9d0fa-226">Örnek DB2 "zaman serisi veri için" zaman damgası"etiketli bir sütun sahip MyTable" adlı bir tablo oluşturduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-226">The sample assumes that you have created a table in DB2 named "MyTable" that has a column labeled "timestamp" for the time series data.</span></span>

<span data-ttu-id="9d0fa-227">**Dış** özelliği ayarlanmış "true"</span><span class="sxs-lookup"><span data-stu-id="9d0fa-227">The **external** property is set to "true."</span></span> <span data-ttu-id="9d0fa-228">Bu ayar, bu veri kümesi data factory dış ve veri fabrikasında bir etkinlik tarafından üretilen değil Data Factory hizmetinin bildirir.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-228">This setting informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="9d0fa-229">Dikkat **türü** özelliği ayarlanmış **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-229">Notice that the **type** property is set to **RelationalTable**.</span></span>


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

<span data-ttu-id="9d0fa-230">**Azure Blob dataset çıktı**</span><span class="sxs-lookup"><span data-stu-id="9d0fa-230">**Azure Blob output dataset**</span></span>

<span data-ttu-id="9d0fa-231">Veri yazıldığı için yeni bir blob saatte ayarlayarak **sıklığı** "Saat" özelliğine ve **aralığı** özelliği 1.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-231">Data is written to a new blob every hour by setting the **frequency** property to "Hour" and the **interval** property to 1.</span></span> <span data-ttu-id="9d0fa-232">**FolderPath** özelliği blob dinamik olarak değerlendirilmesi için işleniyor dilim başlangıç zamanı temel alarak.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-232">The **folderPath** property for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="9d0fa-233">Klasör yolu yıl, ay, gün ve saati başlangıç saatinden bölümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-233">The folder path uses the year, month, day, and hour parts of the start time.</span></span>

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

<span data-ttu-id="9d0fa-234">**Ardışık düzeni için kopyalama etkinliği**</span><span class="sxs-lookup"><span data-stu-id="9d0fa-234">**Pipeline for the copy activity**</span></span>

<span data-ttu-id="9d0fa-235">Ardışık Düzen belirtilen giriş ve çıktı veri kümeleri için yapılandırılmış ve saatte bir çalışacak şekilde zamanlanmış kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-235">The pipeline contains a copy activity that is configured to use specified input and output datasets and which is scheduled to run every hour.</span></span> <span data-ttu-id="9d0fa-236">Ardışık düzeni için JSON tanımında **kaynak** türü ayarlanmış **RelationalSource** ve **havuz** türü ayarlanmış **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-236">In the JSON definition for the pipeline, the **source** type is set to **RelationalSource** and the **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="9d0fa-237">SQL sorgusu için belirtilen **sorgu** özelliği "Siparişler" tablosundan verileri seçer.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-237">The SQL query specified for the **query** property selects the data from the "Orders" table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for the copy activity",
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

## <a name="type-mapping-for-db2"></a><span data-ttu-id="9d0fa-238">DB2 için tür eşlemesi</span><span class="sxs-lookup"><span data-stu-id="9d0fa-238">Type mapping for DB2</span></span>
<span data-ttu-id="9d0fa-239">Bölümünde belirtildiği gibi [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale, kopyalama etkinliği türü aşağıdaki iki aşamalı yaklaşımı kullanarak havuz için kaynak türünden otomatik tür dönüşümleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="9d0fa-239">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type to sink type by using the following two-step approach:</span></span>

1. <span data-ttu-id="9d0fa-240">Yerel kaynak türünden bir .NET türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="9d0fa-240">Convert from a native source type to a .NET type</span></span>
2. <span data-ttu-id="9d0fa-241">Bir .NET türünden bir yerel havuz türüne dönüştürün</span><span class="sxs-lookup"><span data-stu-id="9d0fa-241">Convert from a .NET type to a native sink type</span></span>

<span data-ttu-id="9d0fa-242">Kopya etkinliği bir DB2 türünden bir .NET türü veri dönüştürdüğünde aşağıdaki eşlemelerini kullanılır:</span><span class="sxs-lookup"><span data-stu-id="9d0fa-242">The following mappings are used when Copy Activity converts the data from a DB2 type to a .NET type:</span></span>

| <span data-ttu-id="9d0fa-243">DB2 veritabanı türü</span><span class="sxs-lookup"><span data-stu-id="9d0fa-243">DB2 database type</span></span> | <span data-ttu-id="9d0fa-244">.NET framework türü</span><span class="sxs-lookup"><span data-stu-id="9d0fa-244">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="9d0fa-245">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="9d0fa-245">SmallInt</span></span> |<span data-ttu-id="9d0fa-246">Int16</span><span class="sxs-lookup"><span data-stu-id="9d0fa-246">Int16</span></span> |
| <span data-ttu-id="9d0fa-247">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="9d0fa-247">Integer</span></span> |<span data-ttu-id="9d0fa-248">Int32</span><span class="sxs-lookup"><span data-stu-id="9d0fa-248">Int32</span></span> |
| <span data-ttu-id="9d0fa-249">BigInt</span><span class="sxs-lookup"><span data-stu-id="9d0fa-249">BigInt</span></span> |<span data-ttu-id="9d0fa-250">Int64</span><span class="sxs-lookup"><span data-stu-id="9d0fa-250">Int64</span></span> |
| <span data-ttu-id="9d0fa-251">Real</span><span class="sxs-lookup"><span data-stu-id="9d0fa-251">Real</span></span> |<span data-ttu-id="9d0fa-252">Tek</span><span class="sxs-lookup"><span data-stu-id="9d0fa-252">Single</span></span> |
| <span data-ttu-id="9d0fa-253">Çift</span><span class="sxs-lookup"><span data-stu-id="9d0fa-253">Double</span></span> |<span data-ttu-id="9d0fa-254">Çift</span><span class="sxs-lookup"><span data-stu-id="9d0fa-254">Double</span></span> |
| <span data-ttu-id="9d0fa-255">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="9d0fa-255">Float</span></span> |<span data-ttu-id="9d0fa-256">Çift</span><span class="sxs-lookup"><span data-stu-id="9d0fa-256">Double</span></span> |
| <span data-ttu-id="9d0fa-257">Ondalık</span><span class="sxs-lookup"><span data-stu-id="9d0fa-257">Decimal</span></span> |<span data-ttu-id="9d0fa-258">Ondalık</span><span class="sxs-lookup"><span data-stu-id="9d0fa-258">Decimal</span></span> |
| <span data-ttu-id="9d0fa-259">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="9d0fa-259">DecimalFloat</span></span> |<span data-ttu-id="9d0fa-260">Ondalık</span><span class="sxs-lookup"><span data-stu-id="9d0fa-260">Decimal</span></span> |
| <span data-ttu-id="9d0fa-261">sayısal</span><span class="sxs-lookup"><span data-stu-id="9d0fa-261">Numeric</span></span> |<span data-ttu-id="9d0fa-262">Ondalık</span><span class="sxs-lookup"><span data-stu-id="9d0fa-262">Decimal</span></span> |
| <span data-ttu-id="9d0fa-263">Tarih</span><span class="sxs-lookup"><span data-stu-id="9d0fa-263">Date</span></span> |<span data-ttu-id="9d0fa-264">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="9d0fa-264">DateTime</span></span> |
| <span data-ttu-id="9d0fa-265">Zaman</span><span class="sxs-lookup"><span data-stu-id="9d0fa-265">Time</span></span> |<span data-ttu-id="9d0fa-266">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="9d0fa-266">TimeSpan</span></span> |
| <span data-ttu-id="9d0fa-267">zaman damgası</span><span class="sxs-lookup"><span data-stu-id="9d0fa-267">Timestamp</span></span> |<span data-ttu-id="9d0fa-268">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="9d0fa-268">DateTime</span></span> |
| <span data-ttu-id="9d0fa-269">XML</span><span class="sxs-lookup"><span data-stu-id="9d0fa-269">Xml</span></span> |<span data-ttu-id="9d0fa-270">Byte]</span><span class="sxs-lookup"><span data-stu-id="9d0fa-270">Byte[]</span></span> |
| <span data-ttu-id="9d0fa-271">char</span><span class="sxs-lookup"><span data-stu-id="9d0fa-271">Char</span></span> |<span data-ttu-id="9d0fa-272">Dize</span><span class="sxs-lookup"><span data-stu-id="9d0fa-272">String</span></span> |
| <span data-ttu-id="9d0fa-273">VarChar</span><span class="sxs-lookup"><span data-stu-id="9d0fa-273">VarChar</span></span> |<span data-ttu-id="9d0fa-274">Dize</span><span class="sxs-lookup"><span data-stu-id="9d0fa-274">String</span></span> |
| <span data-ttu-id="9d0fa-275">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="9d0fa-275">LongVarChar</span></span> |<span data-ttu-id="9d0fa-276">Dize</span><span class="sxs-lookup"><span data-stu-id="9d0fa-276">String</span></span> |
| <span data-ttu-id="9d0fa-277">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="9d0fa-277">DB2DynArray</span></span> |<span data-ttu-id="9d0fa-278">Dize</span><span class="sxs-lookup"><span data-stu-id="9d0fa-278">String</span></span> |
| <span data-ttu-id="9d0fa-279">İkili</span><span class="sxs-lookup"><span data-stu-id="9d0fa-279">Binary</span></span> |<span data-ttu-id="9d0fa-280">Byte]</span><span class="sxs-lookup"><span data-stu-id="9d0fa-280">Byte[]</span></span> |
| <span data-ttu-id="9d0fa-281">VarBinary</span><span class="sxs-lookup"><span data-stu-id="9d0fa-281">VarBinary</span></span> |<span data-ttu-id="9d0fa-282">Byte]</span><span class="sxs-lookup"><span data-stu-id="9d0fa-282">Byte[]</span></span> |
| <span data-ttu-id="9d0fa-283">LONGVARBINARY</span><span class="sxs-lookup"><span data-stu-id="9d0fa-283">LongVarBinary</span></span> |<span data-ttu-id="9d0fa-284">Byte]</span><span class="sxs-lookup"><span data-stu-id="9d0fa-284">Byte[]</span></span> |
| <span data-ttu-id="9d0fa-285">Grafiği</span><span class="sxs-lookup"><span data-stu-id="9d0fa-285">Graphic</span></span> |<span data-ttu-id="9d0fa-286">Dize</span><span class="sxs-lookup"><span data-stu-id="9d0fa-286">String</span></span> |
| <span data-ttu-id="9d0fa-287">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="9d0fa-287">VarGraphic</span></span> |<span data-ttu-id="9d0fa-288">Dize</span><span class="sxs-lookup"><span data-stu-id="9d0fa-288">String</span></span> |
| <span data-ttu-id="9d0fa-289">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="9d0fa-289">LongVarGraphic</span></span> |<span data-ttu-id="9d0fa-290">Dize</span><span class="sxs-lookup"><span data-stu-id="9d0fa-290">String</span></span> |
| <span data-ttu-id="9d0fa-291">CLOB</span><span class="sxs-lookup"><span data-stu-id="9d0fa-291">Clob</span></span> |<span data-ttu-id="9d0fa-292">Dize</span><span class="sxs-lookup"><span data-stu-id="9d0fa-292">String</span></span> |
| <span data-ttu-id="9d0fa-293">Blob</span><span class="sxs-lookup"><span data-stu-id="9d0fa-293">Blob</span></span> |<span data-ttu-id="9d0fa-294">Byte]</span><span class="sxs-lookup"><span data-stu-id="9d0fa-294">Byte[]</span></span> |
| <span data-ttu-id="9d0fa-295">DbClob</span><span class="sxs-lookup"><span data-stu-id="9d0fa-295">DbClob</span></span> |<span data-ttu-id="9d0fa-296">Dize</span><span class="sxs-lookup"><span data-stu-id="9d0fa-296">String</span></span> |
| <span data-ttu-id="9d0fa-297">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="9d0fa-297">SmallInt</span></span> |<span data-ttu-id="9d0fa-298">Int16</span><span class="sxs-lookup"><span data-stu-id="9d0fa-298">Int16</span></span> |
| <span data-ttu-id="9d0fa-299">Tamsayı</span><span class="sxs-lookup"><span data-stu-id="9d0fa-299">Integer</span></span> |<span data-ttu-id="9d0fa-300">Int32</span><span class="sxs-lookup"><span data-stu-id="9d0fa-300">Int32</span></span> |
| <span data-ttu-id="9d0fa-301">BigInt</span><span class="sxs-lookup"><span data-stu-id="9d0fa-301">BigInt</span></span> |<span data-ttu-id="9d0fa-302">Int64</span><span class="sxs-lookup"><span data-stu-id="9d0fa-302">Int64</span></span> |
| <span data-ttu-id="9d0fa-303">Real</span><span class="sxs-lookup"><span data-stu-id="9d0fa-303">Real</span></span> |<span data-ttu-id="9d0fa-304">Tek</span><span class="sxs-lookup"><span data-stu-id="9d0fa-304">Single</span></span> |
| <span data-ttu-id="9d0fa-305">Çift</span><span class="sxs-lookup"><span data-stu-id="9d0fa-305">Double</span></span> |<span data-ttu-id="9d0fa-306">Çift</span><span class="sxs-lookup"><span data-stu-id="9d0fa-306">Double</span></span> |
| <span data-ttu-id="9d0fa-307">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="9d0fa-307">Float</span></span> |<span data-ttu-id="9d0fa-308">Çift</span><span class="sxs-lookup"><span data-stu-id="9d0fa-308">Double</span></span> |
| <span data-ttu-id="9d0fa-309">Ondalık</span><span class="sxs-lookup"><span data-stu-id="9d0fa-309">Decimal</span></span> |<span data-ttu-id="9d0fa-310">Ondalık</span><span class="sxs-lookup"><span data-stu-id="9d0fa-310">Decimal</span></span> |
| <span data-ttu-id="9d0fa-311">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="9d0fa-311">DecimalFloat</span></span> |<span data-ttu-id="9d0fa-312">Ondalık</span><span class="sxs-lookup"><span data-stu-id="9d0fa-312">Decimal</span></span> |
| <span data-ttu-id="9d0fa-313">sayısal</span><span class="sxs-lookup"><span data-stu-id="9d0fa-313">Numeric</span></span> |<span data-ttu-id="9d0fa-314">Ondalık</span><span class="sxs-lookup"><span data-stu-id="9d0fa-314">Decimal</span></span> |
| <span data-ttu-id="9d0fa-315">Tarih</span><span class="sxs-lookup"><span data-stu-id="9d0fa-315">Date</span></span> |<span data-ttu-id="9d0fa-316">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="9d0fa-316">DateTime</span></span> |
| <span data-ttu-id="9d0fa-317">Zaman</span><span class="sxs-lookup"><span data-stu-id="9d0fa-317">Time</span></span> |<span data-ttu-id="9d0fa-318">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="9d0fa-318">TimeSpan</span></span> |
| <span data-ttu-id="9d0fa-319">zaman damgası</span><span class="sxs-lookup"><span data-stu-id="9d0fa-319">Timestamp</span></span> |<span data-ttu-id="9d0fa-320">Tarih saat</span><span class="sxs-lookup"><span data-stu-id="9d0fa-320">DateTime</span></span> |
| <span data-ttu-id="9d0fa-321">XML</span><span class="sxs-lookup"><span data-stu-id="9d0fa-321">Xml</span></span> |<span data-ttu-id="9d0fa-322">Byte]</span><span class="sxs-lookup"><span data-stu-id="9d0fa-322">Byte[]</span></span> |
| <span data-ttu-id="9d0fa-323">char</span><span class="sxs-lookup"><span data-stu-id="9d0fa-323">Char</span></span> |<span data-ttu-id="9d0fa-324">Dize</span><span class="sxs-lookup"><span data-stu-id="9d0fa-324">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="9d0fa-325">Kaynak havuzu sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="9d0fa-325">Map source to sink columns</span></span>
<span data-ttu-id="9d0fa-326">Havuz dataset sütunlara kaynak veri kümesinde sütun eşleme hakkında bilgi edinmek için [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="9d0fa-326">To learn how to map columns in the source dataset to columns in the sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="9d0fa-327">İlişkisel kaynaklardan yinelenebilir okuma</span><span class="sxs-lookup"><span data-stu-id="9d0fa-327">Repeatable reads from relational sources</span></span>
<span data-ttu-id="9d0fa-328">İlişkisel veri deposundan verileri kopyaladığınızda, Yinelenebilirlik istenmeyen sonuçları önlemek için göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-328">When you copy data from a relational data store, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="9d0fa-329">Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-329">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="9d0fa-330">Yeniden deneme de yapılandırabilirsiniz **İlkesi** özelliği için bir veri kümesi bir hata oluştuğunda bir dilimi yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-330">You can also configure the retry **policy** property for a dataset to rerun a slice when a failure occurs.</span></span> <span data-ttu-id="9d0fa-331">Aynı veri dilimi yeniden kaç kez olsun ve dilim yeniden nasıl bakılmaksızın okuduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9d0fa-331">Make sure that the same data is read no matter how many times the slice is rerun, and regardless of how you rerun the slice.</span></span> <span data-ttu-id="9d0fa-332">Daha fazla bilgi için bkz: [Repeatable okur ilişkisel kaynaklardan](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="9d0fa-332">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="9d0fa-333">Performans ve ayar</span><span class="sxs-lookup"><span data-stu-id="9d0fa-333">Performance and tuning</span></span>
<span data-ttu-id="9d0fa-334">Kopyalama etkinliği ve performansı iyileştirmek için yollar performansını etkileyen anahtar Etkenler hakkında bilgi edinin [kopya etkinliği performansının ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="9d0fa-334">Learn about key factors that affect the performance of Copy Activity and ways to optimize performance in the [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span>