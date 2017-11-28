---
title: Azure SQL Data Warehouse aaaLoad verisine | Microsoft Docs
description: "Merhaba ortak senaryolar için veri SQL Data Warehouse'a veri yükleme hakkında bilgi edinin. Bunlar PolyBase, Azure blob depolama, düz dosyalar ve disk sevkiyat kullanarak içerir. Üçüncü taraf araçları da kullanabilirsiniz."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="69295-105">Azure SQL Data Warehouse'a veri yükleme</span><span class="sxs-lookup"><span data-stu-id="69295-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="69295-106">Merhaba senaryo seçenekleri ve SQL Data Warehouse'a veri yükleme ile ilgili öneriler özeti.</span><span class="sxs-lookup"><span data-stu-id="69295-106">A summary of hello scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="69295-107">veri yükleme hello en zor bir parçası genellikle hello veri hello yük için hazırlanıyor.</span><span class="sxs-lookup"><span data-stu-id="69295-107">hello hardest part of loading data is usually preparing hello data for hello load.</span></span> <span data-ttu-id="69295-108">Azure yükleme Azure blob depolama ortak bir veri deposu olarak pek çok hello Hizmetleri kullanarak basitleştirir ve Azure Data Factory kullanarak tooorchestrate iletişim ve veri taşıma arasında hello Azure Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="69295-108">Azure simplifies loading by using Azure blob storage as a common data store for many of hello services, and using Azure Data Factory tooorchestrate communication and data movement between hello Azure services.</span></span> <span data-ttu-id="69295-109">Bu işlemler, SQL Data Warehouse'a (MPP) tooload verileri Azure blob depolama biriminden paralel yüksek düzeyde paralel işleme kullanan PolyBase teknolojisi ile tümleştirilir.</span><span class="sxs-lookup"><span data-stu-id="69295-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) tooload data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="69295-110">Örnek veritabanları yükleme öğreticileri için bkz: [örnek veritabanları yükleme][Load sample databases].</span><span class="sxs-lookup"><span data-stu-id="69295-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="69295-111">Azure blob depolama alanından yükleme</span><span class="sxs-lookup"><span data-stu-id="69295-111">Load from Azure blob storage</span></span>
<span data-ttu-id="69295-112">Merhaba hızlı şekilde tooimport SQL veri ambarında toouse PolyBase tooload verileri Azure blob depolama biriminden verilerdir.</span><span class="sxs-lookup"><span data-stu-id="69295-112">hello fastest way tooimport data into SQL Data Warehouse is toouse PolyBase tooload data from Azure blob storage.</span></span> <span data-ttu-id="69295-113">PolyBase kullanan SQL Data Warehouse's (MPP) tasarım tooload verileri Azure blob depolama biriminden paralel yüksek düzeyde paralel işleme.</span><span class="sxs-lookup"><span data-stu-id="69295-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design tooload data in parallel from Azure blob storage.</span></span> <span data-ttu-id="69295-114">toouse PolyBase, T-SQL komutlarıyla veya bir Azure Data Factory işlem hattı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69295-114">toouse PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="69295-115">1. PolyBase ve T-SQL kullanın</span><span class="sxs-lookup"><span data-stu-id="69295-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="69295-116">Yükleme işlemi özeti:</span><span class="sxs-lookup"><span data-stu-id="69295-116">Summary of loading process:</span></span>

1. <span data-ttu-id="69295-117">Veri tooAzure blob depolama veya Azure Data Lake Store taşıyın ve metin dosyalarında depolar.</span><span class="sxs-lookup"><span data-stu-id="69295-117">Move your data tooAzure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="69295-118">SQL veri ambarı toodefine hello konumu ve hello veri biçimini dış nesneleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="69295-118">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data</span></span>
3. <span data-ttu-id="69295-119">Bir T-SQL komut tooload hello verileri paralel olarak yeni bir veritabanı tablosuna çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="69295-119">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="69295-120">Bir öğretici için bkz: [Azure blob depolama tooSQL veri ambarı (PolyBase) veri yükleme][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="69295-120">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="69295-121">2. Azure Data Factory'i kullanma</span><span class="sxs-lookup"><span data-stu-id="69295-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="69295-122">Bir basit yol toouse için PolyBase, Azure blob depolama biriminden PolyBase tooload verileri SQL Data Warehouse'a veri kullanan bir Azure Data Factory işlem hattı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69295-122">For a simpler way toouse PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase tooload data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="69295-123">Toodefine hello T-SQL nesneleri gerekmeyen beri hızlı tooconfigure budur.</span><span class="sxs-lookup"><span data-stu-id="69295-123">This is fast tooconfigure since you don't need toodefine hello T-SQL objects.</span></span> <span data-ttu-id="69295-124">İçe aktarmadan tooquery hello dış veri ihtiyacınız varsa, T-SQL kullanın.</span><span class="sxs-lookup"><span data-stu-id="69295-124">If you need tooquery hello external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="69295-125">Yükleme işlemi özeti:</span><span class="sxs-lookup"><span data-stu-id="69295-125">Summary of loading process:</span></span>

1. <span data-ttu-id="69295-126">Veri tooAzure blob depolama alanınızın taşıyın ve metin dosyalarında depolar.</span><span class="sxs-lookup"><span data-stu-id="69295-126">Move your data tooAzure blob storage and store it in text files.</span></span> <span data-ttu-id="69295-127">Azure Data Factory şu anda PolyBase ile ADLS bağlantısı desteklemez).</span><span class="sxs-lookup"><span data-stu-id="69295-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="69295-128">Bir Azure Data Factory işlem hattı tooingest hello veri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="69295-128">Create an Azure Data Factory pipeline tooingest hello data.</span></span> <span data-ttu-id="69295-129">Merhaba PolyBase seçeneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="69295-129">Use hello PolyBase option.</span></span>
4. <span data-ttu-id="69295-130">Zamanlama ve hello ardışık düzen çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="69295-130">Schedule and run hello pipeline.</span></span>

<span data-ttu-id="69295-131">Bir öğretici için bkz: [Azure blob depolama tooSQL veri ambarı (Azure Data Factory) veri yükleme][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].</span><span class="sxs-lookup"><span data-stu-id="69295-131">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="69295-132">SQL Server'dan yükleme</span><span class="sxs-lookup"><span data-stu-id="69295-132">Load from SQL Server</span></span>
<span data-ttu-id="69295-133">SQL Server tooSQL veri ambarı Integration Services (SSIS), kullanabileceğiniz tooload verileri düz dosya aktarımı veya diskleri tooMicrosoft sevk.</span><span class="sxs-lookup"><span data-stu-id="69295-133">tooload data from SQL Server tooSQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks tooMicrosoft.</span></span> <span data-ttu-id="69295-134">Üzerinde toosee hello işlemleri ve bağlantıları tootutorials yüklenirken farklı özetini okuyun.</span><span class="sxs-lookup"><span data-stu-id="69295-134">Read on toosee a summary of hello different loading processes and links tootutorials.</span></span>

<span data-ttu-id="69295-135">tooplan veri ambarı, SQL Server tooSQL tam veri geçişini bkz hello [geçişine genel bakış][Migration overview].</span><span class="sxs-lookup"><span data-stu-id="69295-135">tooplan a full data migration from SQL Server tooSQL Data Warehouse, see hello [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="69295-136">Integration Services (SSIS) kullanın</span><span class="sxs-lookup"><span data-stu-id="69295-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="69295-137">İçinde SQL Server Integration Services (SSIS) paketleri tooload zaten kullanıyorsanız, paketleri toouse SQL Server hello kaynak ve SQL Data Warehouse hello hedef olarak olarak güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69295-137">If you are already using Integration Services (SSIS) packages tooload into SQL Server, you can update your packages toouse SQL Server as hello source and SQL Data Warehouse as hello destination.</span></span> <span data-ttu-id="69295-138">Bu hızlı ve kolay toodo ve, yükleme toomigrate çalışmıyorsanız iyi bir seçimdir işlem zaten hello bulutta toouse veri.</span><span class="sxs-lookup"><span data-stu-id="69295-138">This is quick and easy toodo, and is a good choice if you are not trying toomigrate your loading process toouse data already in hello cloud.</span></span> <span data-ttu-id="69295-139">Merhaba kolaylığını hello yük bu SSIS paralel olarak hello yük gerçekleştirmez çünkü PolyBase kullanmaktan daha yavaş olacaktır ' dir.</span><span class="sxs-lookup"><span data-stu-id="69295-139">hello tradeoff is hello load will be slower than using PolyBase because this SSIS does not perform hello load in parallel.</span></span>

<span data-ttu-id="69295-140">Yükleme işlemi özeti:</span><span class="sxs-lookup"><span data-stu-id="69295-140">Summary of loading process:</span></span>

1. <span data-ttu-id="69295-141">Integration Services paketini toopoint toohello SQL Server örneğinizi hello kaynağı için ve hello SQL Data Warehouse veritabanı hello hedef için gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="69295-141">Revise your Integration Services package toopoint toohello SQL Server instance for hello source and hello SQL Data Warehouse database for hello destination.</span></span>
2. <span data-ttu-id="69295-142">Bunu zaten yoksa, şema tooSQL veri ambarı geçirin.</span><span class="sxs-lookup"><span data-stu-id="69295-142">Migrate your schema tooSQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="69295-143">Değişiklik hello paketlerinizi eşlemesindeki SQL Data Warehouse tarafından desteklenen hello veri türlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="69295-143">Change hello mapping in your packages use only hello data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="69295-144">Zamanlama ve hello paketini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="69295-144">Schedule and run hello package.</span></span>

<span data-ttu-id="69295-145">Bir öğretici için bkz: [SQL veri ambarı (SSIS) SQL Server tooAzure veri yükleme][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].</span><span class="sxs-lookup"><span data-stu-id="69295-145">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="69295-146">AZCopy (< 10 TB veri için önerilir) kullanın</span><span class="sxs-lookup"><span data-stu-id="69295-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="69295-147">Veri boyutu < 10 TB ise, hello veri SQL Server tooflat dosyalarından dışarı aktarabilir, hello dosyaları tooAzure blob depolama kopyalayın ve sonra PolyBase tooload hello verileri SQL Data Warehouse'a kullanın</span><span class="sxs-lookup"><span data-stu-id="69295-147">If your data size is < 10 TB, you can export hello data from SQL Server tooflat files, copy hello files tooAzure blob storage, and then use PolyBase tooload hello data into SQL Data Warehouse</span></span>

<span data-ttu-id="69295-148">Yükleme işlemi özeti:</span><span class="sxs-lookup"><span data-stu-id="69295-148">Summary of loading process:</span></span>

1. <span data-ttu-id="69295-149">Merhaba bcp komut satırı yardımcı programını tooexport verileri SQL Server tooflat dosyalarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="69295-149">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="69295-150">Düz dosyalar tooAzure blob depolama biriminden Hello AZCopy komut satırı yardımcı programını toocopy verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="69295-150">Use hello AZCopy command-line utility toocopy data from flat files tooAzure blob storage.</span></span>
3. <span data-ttu-id="69295-151">PolyBase tooload SQL Data Warehouse'a kullanın.</span><span class="sxs-lookup"><span data-stu-id="69295-151">Use PolyBase tooload into SQL Data Warehouse.</span></span>

<span data-ttu-id="69295-152">Bir öğretici için bkz: [Azure blob depolama tooSQL veri ambarı (PolyBase) veri yükleme][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="69295-152">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="69295-153">BCP kullanın</span><span class="sxs-lookup"><span data-stu-id="69295-153">Use bcp</span></span>
<span data-ttu-id="69295-154">Az miktarda veriniz varsa, doğrudan Azure SQL Data Warehouse'a bcp tooload kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69295-154">If you have a small amount of data you can use bcp tooload directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="69295-155">Yükleme işlemi özeti:</span><span class="sxs-lookup"><span data-stu-id="69295-155">Summary of loading process:</span></span>

1. <span data-ttu-id="69295-156">Merhaba bcp komut satırı yardımcı programını tooexport verileri SQL Server tooflat dosyalarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="69295-156">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="69295-157">Bcp tooload verileri düz kullan doğrudan tooSQL veri ambarı dosyaları.</span><span class="sxs-lookup"><span data-stu-id="69295-157">Use bcp tooload data from flat files directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="69295-158">Bir öğretici için bkz: [SQL veri ambarı (bcp) SQL Server tooAzure veri yükleme][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].</span><span class="sxs-lookup"><span data-stu-id="69295-158">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="69295-159">İçeri/dışarı aktarma (> 10 TB veri için önerilir) kullanın</span><span class="sxs-lookup"><span data-stu-id="69295-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="69295-160">Veri boyutu > 10 TB'tır ve toomove istiyorsanız bunu tooAzure, öneririz hizmet sevkiyat bizim disk kullanmak [içeri/dışarı aktarma][Import/Export].</span><span class="sxs-lookup"><span data-stu-id="69295-160">If your data size is > 10 TB and you want toomove it tooAzure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="69295-161">Yükleme işlemi özeti</span><span class="sxs-lookup"><span data-stu-id="69295-161">Summary of loading process</span></span>

1. <span data-ttu-id="69295-162">SQL Server tooflat dosyalarından aktarılabilir disklerde Hello bcp komut satırı yardımcı programını tooexport verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="69295-162">Use hello bcp command-line utility tooexport data from SQL Server tooflat files on transferrable disks.</span></span>
2. <span data-ttu-id="69295-163">Merhaba diskleri tooMicrosoft birlikte.</span><span class="sxs-lookup"><span data-stu-id="69295-163">Ship hello disks tooMicrosoft.</span></span>
3. <span data-ttu-id="69295-164">Microsoft hello verileri SQL Data Warehouse'a veri yükler.</span><span class="sxs-lookup"><span data-stu-id="69295-164">Microsoft loads hello data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="69295-165">Hdınsight'ta yükleme</span><span class="sxs-lookup"><span data-stu-id="69295-165">Load from HDInsight</span></span>
<span data-ttu-id="69295-166">SQL veri ambarı veri PolyBase aracılığıyla hdınsight'tan destekler.</span><span class="sxs-lookup"><span data-stu-id="69295-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="69295-167">Hello işlemi olan hello PolyBase tooconnect tooHDInsight tooload verileri kullanarak olan Azure Blob depolama alanından - verileri yüklenirken aynıdır.</span><span class="sxs-lookup"><span data-stu-id="69295-167">hello process is hello same as loading data from Azure Blob Storage - using PolyBase tooconnect tooHDInsight tooload data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="69295-168">1. PolyBase ve T-SQL kullanın</span><span class="sxs-lookup"><span data-stu-id="69295-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="69295-169">Yükleme işlemi özeti:</span><span class="sxs-lookup"><span data-stu-id="69295-169">Summary of loading process:</span></span>

1. <span data-ttu-id="69295-170">Veri tooHDInsight taşıyın ve metin dosyalarını saklamak ORC veya Parquet biçimi.</span><span class="sxs-lookup"><span data-stu-id="69295-170">Move your data tooHDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="69295-171">Dış nesneleri, SQL Data Warehouse toodefine hello konumu ve hello veri biçimini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="69295-171">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data.</span></span>
3. <span data-ttu-id="69295-172">Bir T-SQL komut tooload hello verileri paralel olarak yeni bir veritabanı tablosuna çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="69295-172">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<span data-ttu-id="69295-173">Bir öğretici için bkz: [Azure blob depolama tooSQL veri ambarı (PolyBase) veri yükleme][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="69295-173">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="69295-174">Öneriler</span><span class="sxs-lookup"><span data-stu-id="69295-174">Recommendations</span></span>
<span data-ttu-id="69295-175">Ortaklarımızın çoğunun çözümleri yüklenirken vardır.</span><span class="sxs-lookup"><span data-stu-id="69295-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="69295-176">Daha fazla bilgi, toofind listesini görmek bizim [çözüm ortakları][solution partners].</span><span class="sxs-lookup"><span data-stu-id="69295-176">toofind out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="69295-177">Verilerinizi ilişkisel olmayan bir kaynaktan geldiğinden ve içine SQL veri ambarı tooload tootransform gerekir istiyorsanız satırları ve sütunları, yükleme önce içine.</span><span class="sxs-lookup"><span data-stu-id="69295-177">If your data is coming from a non-relational source and you want tooload it into SQL Data Warehouse you will need tootransform it into rows and columns before you load it.</span></span> <span data-ttu-id="69295-178">Dönüştürülen hello verileri veritabanında depolanan toobe gerek yoktur, metin dosyalarından depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="69295-178">hello transformed data doesn't need toobe stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="69295-179">Yeni yüklenen verilere ilişkin istatistikler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="69295-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="69295-180">Azure SQL Data Warehouse henüz istatistiklerin otomatik olarak oluşturulup güncelleştirilmesini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="69295-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="69295-181">Sipariş tooget hello en iyi performans, sorgularından, tüm tabloların hello sonra tüm sütunları toocreate istatistik ilk yükleme veya hello verilerde önemli değişikliklerden önemlidir.</span><span class="sxs-lookup"><span data-stu-id="69295-181">In order tooget hello best performance from your queries, it's important toocreate statistics on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="69295-182">Ayrıntılar için bkz [istatistikleri][Statistics].</span><span class="sxs-lookup"><span data-stu-id="69295-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="69295-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="69295-183">Next steps</span></span>
<span data-ttu-id="69295-184">Daha fazla geliştirme ipuçları için bkz: Merhaba [geliştirmeye genel bakış][development overview].</span><span class="sxs-lookup"><span data-stu-id="69295-184">For more development tips, see hello [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
